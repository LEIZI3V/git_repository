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
* 在GitHub中创建SSH key 和对应的仓库

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

# links
[link1]:assets/markdown-img-paste-20180823085709513.png
