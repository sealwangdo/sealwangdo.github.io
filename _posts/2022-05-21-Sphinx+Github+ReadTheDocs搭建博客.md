---
layout: post
title: "Sphinx+Github+ReadTheDocs搭建博客教程"
date: 2022-05-20
tags: [成长, 总结, 博客]
description: [ReadTheDocs搭建博客入门，及遇到的问题]
---

## 准备条件

* Github账号，使用github对文档进行版本管理
* 注册Read the Docs账号，官网地址：https://readthedocs.org/
* 安装Python，Sphinx是一个python工具，用于生成文档，所以需要安装Python环境。

## Sphinx创建文档

Sphinx是一个基于Python的文档生成项目，开始是用来生成 Python 官方文档的工具，更多介绍可参考官网：https://www.sphinx.org.cn/ 。

### 安装Sphinx

Sphinx的GitHub地址：https://github.com/sphinx-doc/sphinx

pip安装Sphinx

```
$ pip install sphinx
```

### 创建文档

先将远程github仓库clone到本地，这个仓库是你要托管文档的仓库，如果没有就新建一个。

clone到本地后，在项目根目录创建一个docs目录，cd进入docs目录，执行如下命令：

```
$ sphinx-quickstart
```

输出结果如下：

  ```
  Welcome to the Sphinx 4.2.0 quickstart utility.
  
  Please enter values for the following settings (just press Enter to
  accept a default value, if one is given in brackets).
  
  Selected root path: .
  
  You have two options for placing the build directory for Sphinx output.
  Either, you use a directory "_build" within the root path, or you separate
  "source" and "build" directories within the root path.
  
  > Separate source and build directories (y/n) [n]: y
  
  The project name will occur in several places in the built documentation.
  
  > Project name:seal-note
  > Author name(s): seal
  > Project release []: v1.0
  
  If the documents are to be written in a language other than English,
  you can select a language here by its language code. Sphinx will then
  translate text that it generates into that language.
  
  For a list of supported codes, see
  https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language.
  
  > Project language [en]: zh_CN
  
  Creating file D:\pythonproj\devtest\source\conf.py.
  Creating file D:\pythonproj\devtest\source\index.rst.
  Creating file D:\pythonproj\devtest\Makefile.
  Creating file D:\pythonproj\devtest\make.bat.
  
  Finished: An initial directory structure has been created.
  
  You should now populate your master file D:\pythonproj\devtest\source\index.rst and create other documentation
  source files. Use the Makefile to build the docs, like so:
     make builder
  where "builder" is one of the supported builders, e.g. html, latex or linkcheck.
  ```

上面的配置可以选择默认，稍后修改生成的conf.py配置文件即可。

设置完成后，目录结构如下：

```
  |____Makefile
  |____source
  | |____index.rst
  | |_____templates
  | |____conf.py
  | |_____static
  |____README.md
  |____make.bat
  |____.gitattributes
  |____build
```

build 存放编译后的文件
source/_static 存放静态文件
source/_templates 存放模板文件
source/conf.py 项目配置文件，上面的配置可以在这里面修改
source/index.rst 首页

### 编译

对rst文件进行编译生成HTML及相关静态文件：

  ```
  $ make html
  ```

  ```
  Running Sphinx v4.2.0
  loading translations [zh_CN]... done
  making output directory... done
  building [mo]: targets for 0 po files that are out of date
  building [html]: targets for 1 source files that are out of date
  updating environment: [new config] 1 added, 0 changed, 0 removed
  reading sources... [100%] index
  looking for now-outdated files... none found
  pickling environment... done
  checking consistency... done
  preparing documents... done
  writing output... [100%] index
  generating indices... genindex done
  writing additional pages... search done
  copying static files... done
  copying extra files... done
  dumping search index in Chinese (code: zh)... done
  dumping object inventory... done
  build succeeded.
  
  The HTML pages are in build\html.
  ```

index.rst文件内容会编译到_build/html目录下。_  

打开_build\html\index.html文件，下面是渲染出来的HTML页面：  ![image-20220517155947733](https://tva1.sinaimg.cn/large/e6c9d24egy1h2bgkm6eibj21jk0hmmzg.jpg)

## 配置主题

安装sphinx Read the Docs主题

```
pip install sphinx_rtd_theme
```

更多主题可到官网 https://sphinx-themes.org/ 查看。

配置source/conf.py 文件：

```
import sphinx_rtd_theme
html_theme = "sphinx_rtd_theme"
#html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
html_theme_path = ['/Library/Frameworks/Python.framework/Versions/3.10/lib/python3.10/site-packages']
```

重新编译：

```
$ make html
```

打开_build\html\index.html文件，可以发现主题配置成功。

![image-20220517160249323](https://tva1.sinaimg.cn/large/e6c9d24egy1h2bgnnugfhj21o00n0tbg.jpg)

## 配置markdown

Sphinx默认使用 reStructuredText 标记语言，由于已经习惯使用markdown进行文档编辑，下面来配置markdown。

### 安装recommonmark插件

```
pip install recommonmark
```

### 安装支持markdown表格的插件

```
pip install sphinx_markdown_tables
```

ReadTheDocs的python环境貌似没有sphinx_markdown_tables，在构建时可能报如下错误

```
ModuleNotFoundError: No module named 'sphinx_markdown_tables'
```

解决方案是在docs目录下新建一个requirements.txt文件，写入如下内容：

```
sphinx-markdown-tables==0.0.15
```

可以使用如下命令，把所有当前环境中使用的包信息汇总到requirements.txt:

```
pip freeze > requirements.txt
```

## 配置source/conf.py 文件

source/conf.py中增加：

```
extensions = ['recommonmark','sphinx_markdown_tables'] 
```

如果提示找不到recommonmark的错误，需要明确安装路径：

```
import sys, os
sys.path.append('/Library/Frameworks/Python.framework/Versions/3.10/lib/python3.10/site-packages/')
extensions = ['recommonmark','sphinx_markdown_tables']
```

在source目录下创建一个md路径，存放markdown文件，将md路径添加到source/index.rst 中，

```
.. cpp-note documentation master file, created by
   sphinx-quickstart on Tue May 17 10:14:10 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to seal's documentation!
====================================
.. toctree::
   :maxdepth: 2
   md/index
```

同时，在md目录下面新建一个index.rst文件，添加markdown文件，将markdow文件添加到index.rst中

```
.. toctree::
​    :maxdepth: 1
​    Sphinx+Github+ReadTheDocs搭建博客.md
```

重新编译即可

## 提交上传

.gitignore文件添加docs/build/目录，不需要上传这个目录。上传：

```
git add .
git commit -m "提交说明"
git push -u origin master
```

## 添加Webhooks

在Read the docs 项目-管理-集成中生成Webhooks：

![image-20220517174758825](https://tva1.sinaimg.cn/large/e6c9d24egy1h2bjp2tsv3j21b60u0n1z.jpg)

生成的Webhooks如下：

![image-20220517175018064](https://tva1.sinaimg.cn/large/e6c9d24egy1h2bjrh9n51j21dy0i4djn.jpg)

![image-20220517174914807](https://tva1.sinaimg.cn/large/e6c9d24egy1h2bjqdti3tj21vg0ke78z.jpg)

将webhooks添加到Github 项目-设置-Webhooks红

![image-20220517174851831](https://tva1.sinaimg.cn/large/e6c9d24egy1h2bjpzeoeaj21dd0u042d.jpg)

剩下的就是根据构建步骤进行构建了，可能会遇到一些问题， 按照步骤解决即可！

## 参考

[Sphinx Configration Documents](https://www.sphinx-doc.org/zh_CN/master/usage/configuration.html)