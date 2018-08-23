# 创建版本库
```
$ git config --global user.name "LEIZI3V"
$ git config --global user.email "naoxiaobai@126.com"
$ pwd
$ cd /d FilePath
$ git init
$ git add file1.txt
$ git add file2.txt
$ git commit -m "wrote a readme file"
```

# 建立远程仓库

```
$ ssh-keygen -t rsa -C "naoxiaobai@126.com"
```
* 可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，
这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥。

* 在GitHub中创建SSH key 和对应的仓库

# 创建完成后复制库的地址
* 可以是https或是ssh key

```
$ git remote add origin https://github.com/LEIZI3V/RepositoryName.git
$ git push -u origin master
```
* 修改文件，更新仓库

```
$ git add filename
$ git commit -m "massage abot Change"
$ git push origin master
```

![操作成功][link1]

# 文件操作

```
$ git status
$ git diff file1.txt  # 查看文件修改信息
$ git log  # 查看日志文件
$ git log --pretty=oneline
```

[link1]:https://github.com/LEIZI3V/git_repository/blob/master/picture/Push_Flash.PNG
