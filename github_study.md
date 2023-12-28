# Git study

## Study website

配置git连接Github:https://blog.csdn.net/qq_42815188/article/details/128735530

git remote add:https://blog.csdn.net/qq_25458977/article/details/87875641

## Mac download Git

```
brew install git
```

## Git command line

### set your username and user email

```
git config --global user.name "你的用户名"
git config --global user.emails "你的邮箱"
```

用户名和邮箱最好是填入你的github用户名和邮箱,下载好git后先进行设置这个

### Git init 

```
git init
```

这个代码将创建一个空的仓库

### Git add . and Git commit -m "提交信息"

```
git add . //是将文件夹所有的文件加入到暂存区 .代表所有文件 如果只需要提交文件夹中一个文件,将文件改为具体的文件名就可以
git commit -m "提交信息" //将暂存区文件上传,"提交信息"为你每次需要的文件信息,简单进行备注,防止忘记.
```

### Git log

```
git log //显示提交的文件记录
```

## 配置Git连接Github

### 1.配置git的用户名和邮箱(已经安装好git,并且注册好GitHub账号)

### 2.远程连接github有两种传输协议

#### 2.1基于SSH协议配置Git连接Github

##### 2.1.1为本机生成密钥对

```
ssh-keygen -t rsa -C "本机标识"
```

这里的命令`-C`只是给产生的密钥生成一个注释,最好填写与本机相关的内容.具体看文章https://www.jianshu.com/p/f3020c04d966

![](/Users/chr777/Library/Application Support/typora-user-images/image-20231229045449384.png)

生成的 SSH 密钥对存储在 `C:\Users\账户名\.ssh`(windows)或者(.\user\\账户名.\\.ssh) 目录下，如下图所示：

![image-20231229045959681](/Users/chr777/Library/Application Support/typora-user-images/image-20231229045959681.png)

其中id_rsa保存的是**私钥**,id_rsa.pub保存的是**公钥**

然后将id_esa.pub中的内容复制粘贴.

```
ssh-keygen -f ~/.ssh/id_rsa -p          //后期可以重新设置passpharse的密码
```

##### 2.1.2将公钥拷贝到 GitHub 上

![image-20231229050842794](/Users/chr777/Library/Application Support/typora-user-images/image-20231229050842794.png)

##### 2.1.3检测ssh连接成功

```
ssh -T git@github.com
```

##### 2.1.4两种方法将本地仓库和远程仓库连接起来

###### 2.1.4.1第一种方法

在Github上创建一个仓库,接着使用下述命令初始化本地仓库,生成.git文件,并默认进入主分支 `main`。

```
git init
```

然后将想要上传的文件放到这个本地仓库文件夹下，执行如下命令将文件添加到本地仓库：

```
git add .
```

接着将文件提交到本地仓库：

```
git commit -m "注释"
```

然后复制远程仓库的 SSH 地址，执行如下命令将本地仓库与远程仓库关联起来，关于 git remote add 命令可以参考[这篇文章](https://blog.csdn.net/qq_25458977/article/details/87875641)。

```
git remote add origin 远程仓库的SSH地址
```

将文件上传到 GitHub 的远程仓库：

```
git push -u origin main
```

###### 2.1.4.2第二种方法

在Github上创建一个仓库

然后执行下述指令直接将远程仓库克隆到本地仓库,会自动生成.git.文件,**此时已经和Github仓库已经关联了**,因此不要使用`git init`和`git remote add origin 远程仓库的SSH地址` 这两条指令.

```
git clone 远程仓库的SSH地址
```

然后将想要上传的文件放到这个本地仓库文件夹下，进入本地仓库目录，依次执行如下命令将文件添加并提交到本地仓库：

```
git add .
git commit -m "注释"
```

最后执行如下命令，将文件上传到 GitHub 的远程仓库：

```
git push -u origin main
```



#### 2.2.基于 HTTPS 协议配置 Git 连接 GitHub

注意：由于访问 GitHub 的网络原因，走 HTTPS 协议可能会出现 git push 失败，建议走 SSH 协议，因此看到这里就可以结束了！

##### 2.2.1创建 GitHub 个人访问令牌

![img](https://img-blog.csdnimg.cn/d8d5a28ac87a46a7bf6f15437726a4e8.png#pic_center)

![img](https://img-blog.csdnimg.cn/255db26c07e44e52919de7e9955d50bf.png#pic_center)

![img](https://img-blog.csdnimg.cn/8a52c98a103b4497a398fa3874893222.png#pic_center)

![img](https://img-blog.csdnimg.cn/f11e9f7b83ef4a86904ae4771d2e39f9.png#pic_center)

![img](https://img-blog.csdnimg.cn/571c091958904fa587b8e1edf7a451e9.png#pic_center)

​	![img](https://img-blog.csdnimg.cn/bc6329d909414fbaa6c32c8740014145.png#pic_center)

##### 2.2.2 有两种方法将本地仓库和远程仓库关联起来

###### 5.2.1 第一种方法

接着执行如下命令初始化一个本地仓库，如下图所示，多出了一个隐藏文件夹 .git，并默认进入主分支 main。

```
git init
```


然后将想要上传的文件放到这个本地仓库文件夹下，执行如下命令将文件添加到本地仓库：

```
git add .
```

如果出现这个警告“LF will be replaced by CRLF the next time Git touches it”，可以直接忽略，具体原因参考这篇文章。

接着将文件提交到本地仓库：

```
git commit -m "注释"
```


然后复制远程仓库的 HTTPS 地址，执行如下命令将本地仓库与远程仓库关联起来

```
git remote add origin 远程仓库的HTTPS地址
```


执行如下命令将文件上传到 GitHub 的远程仓库：

```
git push -u origin main
```

会弹出如下窗口，选择“Token”，将保存好的令牌粘贴进去即可。

![img](https://img-blog.csdnimg.cn/dafa8bc6eb9b41a09da3bb686420e12a.png#pic_center)

![img](https://img-blog.csdnimg.cn/e76fe884b2084736bf97605d24017e0a.png#pic_center)



​	![img](https://img-blog.csdnimg.cn/16b771bb2ad344139d83fe4178b50d91.png#pic_center)

###### 5.2.2 第二种方法

这里就是和SSH的第二种方法和HTTPS的第一种方法结合,使用`git clone HTTPS地址`,后述相同.






