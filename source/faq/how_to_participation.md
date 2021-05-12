## 如何参与该文档的开发

我们鼓励每一个记录下在做项目时所遇到的问题，并将其分享出去.
当再次遇到该问题时，可以来FAQ查找，看看是否有相似问题...


#### 1、拉取文档源码

```c
git clone https://github.com/baronZhou/FAQ_TT.git
```

#### 2、搭建编译文档的环境

**(1) 安装必要工具**
```c
sudo apt install git make python3 python3-pip
```

**(2) 安装依赖包**
```c
pip install -r rquirements.txt
```

**(3) 编译**
```c
make html
```

#### 3、编译后使用浏览器打开
编译后输出build/html/index.html文件，用浏览器打开即可看到漂亮的网页

#### 4、贡献自己的修改

文档的源码都在source目录下，以md文件为主。你可以添加自己的文件，或在原有的文件上修改.
修改之后在github上发起pull request

等待owner merge后，内容合到主干。

然后一天一次，该文档会被自动同步到readthedocs上
readthedocs URL ： https://trustonic-faq.readthedocs.io/en/latest/
