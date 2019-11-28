# 前言

描述基于不同使用场景使用不同方案搭建git服务器的步骤，后续补充

## 使用场景

git仓库的使用分为研发和交付:研发可以检出和更改git仓库项目；交付负责检出git仓库项目打包成为产品进行测试或者交付。

## 方案

基于linux文件系统用户和组的权限进行搭建，并基于ssh协议进行检出和提交：为需要写权限的研发成员创建用户组，然后为仓库及仓库目录下的所有子目录及文件分配权限。

## 场景说明
| 属性 | 说明 |
|:----:| :---:|
| git服务器系统 | linux |
| git服务器IP | 192.168.1.6 |
| 开发组用户 | user1、user2 |
| 交付用户 | user3 |
| 项目目录 | /home/test |

## 步骤
### 1. 添加用户（添加三个用户：user1、user2、user3）
>  ```shell 
>  useradd user1#添加user1
>  passwd user1 #修改user1密码
>  useradd user2#添加user2
>  passwd user2 #修改user2密码
>  useradd user3#添加user3
>  passwd user3 #修改user3密码
>  ```
### 2. 创建用户组（组名devTeam）
>  `groupadd devTeam`
### 3. 添加组用户（user1、user2为开发用户添加到devTeam下）
> ```shell
> gpasswd -a user1 #添加user1
> gpasswd -a user1 #添加user2
> ```
### 4. 创建项目并初始化(项目名称test)
> ```shell
>    mkdir test #创建目录
>    cd test  #进入目录
>    git init --bare #初始化一个空的项目仓库
>    chgrp devTeam test #将test目录所属用户组改为devTeam
>    chmod -R 775 test #将test及所有子文件和目录权限修改为775（所属用户可读写可执行，所属组可读写可执行，其他组和其他用户可度可执行）
> ```
### 5. 根据不同情况做不同处理

>#### 1. user1之前在本地已经开发了一部分(假设本地路径为D:/test,且目录中有一个已经开发的文件code1.java)。
>>user1执行如下一系列操作：
>>```cmd
>>   cd /d D:/test #进入本地项目目录
>>   git init #将项目test初始化为git项目
>>   git add code1.java #添加code1.java
>>   git commit -m "提交code1文件"#git提交
>>   git remote add user1@192.168.1.6:/home/test #添加仓库
>>   git push 推送项目代码到仓库
>>```
>> user2执行如下操作：
>>```cmd
>>   cd /d E:/test #user2本地项目录
>>   git clone user2@192.168.1.6:/home/test #检出项目
>>```
>>之后就是后续的user1，user2正常的提交、检出流程
>
>#### 2. 新建的项目还没开始开发
>>user1执行如下操作：
>>```cmd
>>   cd /d D:/test #user1本地项目录
>>   git clone user1@192.168.1.6:/home/test #检出项目
>>```
>>user2执行如下操作：
>>```cmd
>>   cd /d E:/test #user2本地项目录
>>   git clone user2@192.168.1.6:/home/test #检出项目
>>```
>>之后就是后续的user1，user2正常的提交、检出流程