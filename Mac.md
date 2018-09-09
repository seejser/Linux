## Mac使用tree生成目录结构
Mac下可以使用brew install tree进行安装。安装后，在terminal中输入tree -a便可以查看某个文件夹下的所有文件。

### 常用的命令
当然了，我们的需求肯定不止列出所有文件这么简单。下面介绍几个常用的命令

tree -d 只显示文件夹；
tree -L n 显示项目的层级。n表示层级数。比如想要显示项目三层结构，可以用tree -l 3；
tree -I pattern 用于过滤不想要显示的文件或者文件夹。比如你想要过滤项目中的node_modules文件夹，可以使用tree -I "node_modules"；
tree > tree.md 将项目结构输出到tree.md这个文件。
举个例子，如果我们要显示某个项目下3层的所有文件结构，同时又过滤node_modules文件夹，最后输出到tree.md，可以这么写

```
tree -L 3 -I "node_modules">tree.md
```


更多命令的使用可以查看tree --help。
