---
title: vb.net根据name查找控件
urlname: index-vb-net
tags:
  - vb.net
categories:
  - vb.net
date: 2019-05-27 21:54:47
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> 根据窗体中某个空间的名称，查找控件。

<!-- more -->
### 查找并赋值text和tag的代码
```
    ''' <summary>
    ''' 更改窗体控件中Name的显示文本和tag,可以执行相关动作。用于动态加载广告和链接
    ''' </summary>
    ''' <param name="Ctr">控件可以是from</param>
    ''' <param name="CtrName">控件名称</param>
    ''' <param name="Txt">要更换的文本text,如果为no则不更换</param>
    ''' <param name="Tagx">要更换的tag</param>
    ''' <returns></returns>
    Function ADCxConTxtTag(ByVal Ctr As Control, ByVal CtrName As String, ByVal Txt As String, ByVal Tagx As String, Optional addEvenClick As Boolean = False) As ArrayList
        Dim ResList As New ArrayList

        Dim ConName As String = Ctr.Name
        If LCase(ConName) = LCase(CtrName) Then
            If addEvenClick Then
                '增加自动添加click事件到adaction
                AddHandler Ctr.Click, AddressOf ADAction
            End If
            If Txt <> "no" Then
                Ctr.Text = Txt
                Ctr.Tag = Tagx
            End If
        End If
        ResList.Add(Ctr)
        '考虑到有些控件不能按照control进行查找，但是属于item的范畴时候的提取。
        Dim ConType As String = Ctr.GetType().ToString.Split(".").Last.ToString

        Select Case LCase(ConType)
            Case "statusstrip"
                Dim ConItems As ToolStripItemCollection = CType(Ctr, StatusStrip).Items
                Dim I As Integer
                For I = 0 To ConItems.Count - 1
                    'Debug.WriteLine(ConItems.Item(I).Name)
                    '  Debug.WriteLine(ConItems.Item(I).GetType().ToString)
                    ConName = ConItems.Item(I).Name
                    If LCase(ConName) = LCase(CtrName) Then
                        If addEvenClick Then
                            AddHandler ConItems.Item(I).Click, AddressOf ADAction
                        End If
                        If Txt <> "no" Then
                            ConItems.Item(I).Text = Txt
                            ConItems.Item(I).Tag = Tagx
                        End If
                    End If
                    ResList.Add(ConItems.Item(I))
                Next
            Case "toolstrip"
                Dim ConItems As ToolStripItemCollection = CType(Ctr, ToolStrip).Items
                Dim I As Integer
                For I = 0 To ConItems.Count - 1
                    '    Debug.WriteLine(ConItems.Item(I).Name)
                    'Debug.WriteLine(ConItems.Item(I).GetType().ToString)
                    ConName = ConItems.Item(I).Name
                    If LCase(ConName) = LCase(CtrName) Then
                        If addEvenClick Then
                            AddHandler ConItems.Item(I).Click, AddressOf ADAction
                        End If
                        If Txt <> "no" Then
                            ConItems.Item(I).Text = Txt
                            ConItems.Item(I).Tag = Tagx
                        End If
                    End If
                    ResList.Add(ConItems.Item(I))
                Next

        End Select

        '如果含有子控件
        If Ctr.HasChildren Then
            For Each c As Control In Ctr.Controls
                ADCxConTxtTag(c, CtrName, Txt, Tagx, addEvenClick)
            Next c
        End If
        Return ResList
    End Function
```

### 查找一个
```
    ''' <summary>
    ''' 查找Name的控件
    ''' </summary>
    ''' <param name="Ctr">控件可以是from</param>
    ''' <param name="CtrName">控件名称</param>
    ''' <param name="Txt">要更换的文本text,如果为no则不更换</param>
    ''' <param name="Tagx">要更换的tag</param>
    ''' <returns></returns>
    Function GetFrmCtr(ByVal Ctr As Control, ByVal CtrName As String)
        Dim ResList As New ArrayList
        'Dim CtrList As New ArrayList+
        Dim myCtr

        Dim ConName As String = Ctr.Name
        If LCase(ConName) = LCase(CtrName) Then
            'CtrList.Add（Ctr)
            myCtr = Ctr
            AddHandler Ctr.Click, AddressOf ADAction
        End If
        ResList.Add(Ctr)
        '考虑到有些控件不能按照control进行查找，但是属于item的范畴时候的提取。
        Dim ConType As String = LCase(Ctr.GetType().ToString.Split(".").Last.ToString)
        Dim ConItems As System.Windows.Forms.ToolStripItemCollection

        If ConType = "statusstrip" Then
            ConItems = CType(Ctr, StatusStrip).Items
        ElseIf ConType = "toolstrip" Then
            ConItems = CType(Ctr, ToolStrip).Items
        End If

        If Not ConItems Is Nothing Then
            If ConType = "statusstrip" Or ConType = "toolstrip" Then
                Dim I As Integer
                For I = 0 To ConItems.Count - 1
                    'Debug.WriteLine(ConItems.Item(I).Name)
                    '  Debug.WriteLine(ConItems.Item(I).GetType().ToString)
                    ConName = ConItems.Item(I).Name
                    If LCase(ConName) = LCase(CtrName) Then
                        'CtrList.Add（ConItems.Item(I))
                        myCtr = ConItems.Item(I)
                        AddHandler ConItems.Item(I).Click, AddressOf ADAction
                    End If
                    'ResList.Add(ConItems.Item(I))
                Next
            End If
        End If

        '如果含有子控件
        If Ctr.HasChildren Then
            For Each c As Control In Ctr.Controls
                GetFrmCtr(c, CtrName)
            Next c
        End If

        Return myCtr

    End Function
```