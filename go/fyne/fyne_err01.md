最近在学习fyne开发GUI，今天遇到一个奇怪的问题，午休在公司电脑（win7）上编写的程序，编译/运行都没有问题，之后提交到GitHub联系仓库，晚上回来从GitHub上拉下来，在自己电脑（win10）本地编译居然报错
```window.c:640:1: error: converting to execution character set：Illegal byte sequence```后来想起来我的用户路径为中文，后来参考这位老哥的博客[win10环境下更改用户文件夹名](https://blog.csdn.net/qq_38541968/article/details/81450455)把用户路径改为英文的就可以正常运行了，血的教训，不要起中文名！！！
