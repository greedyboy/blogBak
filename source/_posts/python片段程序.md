---
title: python片段程序
urlname: python-pick-index
tags:
  - python
categories:
  - 软件列表
date: 2019-11-16 22:32:27
---
<!-- Hexo daybreak git vb.net 健康 博客设置 网络日志 软件列表 魔法书签 -->
<!--![图]() -->
<!--[]() -->

> python程序小结。

<!-- more -->

### 给图片加玻璃
```
from PIL import Image
import re

#给图片添加一层蒙版，可以设置位置，尺寸，颜色，透明度
def img_add_glass(img,new_img='glass',glass_factor=0.3,glass_color='#ffffff',glass_x=0,glass_y=0,glass_width=300,glass_height=100):
    image=object
    if isinstance(img,str):
        image= Image.open(img)
        if new_img=='myself':
            new_img=img
        elif new_img=='glass':
            new_img=img+'_glass.png'
    else:
        image=img
        # 转换为rgba模式
    image.convert('RGBA')
    # 产生白色底部图片
    glass_color_r, glass_color_g, glass_color_b = toRgb(glass_color)
    img_blank = Image.new('RGBA', (glass_width, glass_height), (glass_color_r, glass_color_g, glass_color_b, int(255 * glass_factor)))
    r, g, b, a = img_blank.split()
    #粘贴图片蒙版
    image.paste(img_blank, (glass_x, glass_y), mask=a)
    #保存img

    #如果是图像对象就返回对象，不保存
    if isinstance(img, str):
        image.save(new_img)
    else:
        new_img=image

    return new_img

    pass
def toRgb(colorhex):
    #转16进制转rgb
    #rx, gx, bx = toRgb('#FFFAF0')
    if not colorhex.startswith('#'):
        colorhex='#'+ colorhex

    opt = re.findall(r'(.{2})',colorhex[1:]) #将字符串两两分割
    rgb = []                        #用以存放最后结果
    for i in range (0, len(opt)):   #for循环，遍历分割后的字符串列表
        rgb.append(int(opt[i], 16))
    #print(rgb)             #输出最后结果，末尾的","不打印
    return rgb


# img='./chunks/tempb.png'
#
# factor=0.2
# #转换为rgba模式
# image2 = Image.open(img)
# image2 = image2.convert('RGBA')
#
# #产生白色底部图片
# img_blank=Image.new('RGBA', (1080,200), (0,255,255,int(255*factor)))
# r,g,b,a=img_blank.split()
#
# image2.paste(img_blank,(0,1700),mask=a)
#
# image2.save('./chunks/text.png')




#rx,gx,bx=toRgb('#FFFAF0')

#print ([rx,gx,bx])

img='./chunks/txt.jpg'
new_img='./chunks/texts.png'
img_add_glass(img=img,new_img=new_img,glass_width=2180,glass_height=300,glass_x=0,glass_y=1000)

```

### 解析字符串到字典形式

```
def eqstr2json(equstr):
    '''
    解析"a=b,c=d形式的字符串到词典，用于参数引入和设置
    :param equstr: a=b,c=d
    :return: {'a': 'b','c':'d'}
    '''
    '''"'''
    orders=equstr.split(',')
    orderjsons=''
    for order in orders:
        print(order)
        print(order.count('=')==1)
        if order and '=' in order and not str(order).startswith("=") and order.count('=')==1 :
            orderjsons=orderjsons+'"'+ order.replace('=','":"')+'",'

    orderjsons='{'+orderjsons[:-1]+'}'

    # print(orderjsons)
    orderjson=json.loads(orderjsons)
    # print(orderjson)


    return orderjsons
```

### pyqt中加载图片和文字对话框
```
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *

import json,sys
class filedialogdemo(QWidget):

    def __init__(self, parent=None):
        super(filedialogdemo, self).__init__(parent)
        layout = QVBoxLayout()

        self.btn = QPushButton()
        self.btn.clicked.connect(self.loadFile)
        self.btn.setText("从文件中获取照片")
        layout.addWidget(self.btn)

        self.label = QLabel()
        layout.addWidget(self.label)

        self.btn_2 = QPushButton()
        self.btn_2.clicked.connect(self.load_text)
        self.btn_2.setText("加载电脑文本文件")
        layout.addWidget(self.btn_2)

        self.content = QTextEdit()
        layout.addWidget(self.content)
        self.setWindowTitle("测试")

        self.setLayout(layout)

    def loadFile(self):
        print("load--file")
        fname, _ = QFileDialog.getOpenFileName(self, '选择图片', 'E:\\PycharmProjects\\untitled2\\imges\\img', 'Image files(*.jpg *.gif *.png)')
        self.label.setPixmap(QPixmap(fname))

    def load_text(self):
        print("load--text")
        dlg = QFileDialog()
        dlg.setFileMode(QFileDialog.AnyFile)
        dlg.setFilter(QDir.Files)
        if dlg.exec_():
            filenames = dlg.selectedFiles()
            f = open(filenames[0], 'r')
            with f:
                data = f.read()
                self.content.setText(data)

if __name__ == '__main__':
    app = QApplication(sys.argv)
    fileload =  filedialogdemo()
    fileload.show()
    sys.exit(app.exec_())
```

python E:\迅雷下载\pycrypto-2.6.1\pycrypto-2.6.1\setup.py install 