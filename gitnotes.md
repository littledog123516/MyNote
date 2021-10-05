# Git学习笔记

## 1.设置Git

```shell
git config --global user.name "Chunli Jiang"  		//global全局设置
git config --global user.email "190488762@qq.com"
git config --local user.name "Chunli Jiang"   		//local对该项目设定特定的作者
```

## 2.更换编辑器

```shell
git config --global core.editor emacs		//默认是vim 可以改成VSCOde
```

## 3.新增初始Repository

```shell
cd practice
git init
```

## 4.把文件交由Git管理

```shell
git add name.xxx
```

把这个文件提交到暂存区，可以使用git来追踪了。

## 5.将暂存区的内容永久保存下

```shell
git commit -m"xxx"
```

 把暂存区的内容保存到存储库（远端）     

## 6.缩短两段式

```shell
git commit -a -m"xxx"
```

等于先add再commit

 ## 7.找到某个人的commit

```shell
git log --oneline --author="xxx"
```

## 8.找到commit信息中是否包含某些关键字

```shell
git log --oneline --grep="xxx"
```

## 9.变更或者删除文件

```shell
git rm xxx.xxx
git mv xxx.xxx xxx.xxx
```

git rm=rm+add节省一步操作

## 10.修改commit记录

改动commit的comment记录有几种方法：

1.如果是修改最后一次commit记录 

```shell
git commit --amend -m"xxxxxx"
```

2.git rebase改动历史纪录

3.git reset删除commit 整理后重新commit

## 11.追加文件到最近一次的commit

1.使用git reset命令删除上一次的commit 加入文件后重新commit

2.使用--amend

```shell
git add xxx.xxx
git commit --amend --no-edit
```

## 12.解除git对某一文件的管理

```shell
git rm xxx --cached
```

## 13.查看某一行代码是谁写的

```shell
git blame xxx.xxx
git blame -L 5,10 xxx.xxx		//5-10行是谁写的
```

## 14.恢复被删除的文件

前提是没有git add呢，目前被删除还只是再工作区被删除，没有提交到暂存区

```shell
git status
git checkout .		//恢复所有删除的文件
git checkout xxx.xxx		//恢复某一文件 
```

这个技巧也可以用于恢复到某一次commit之后的状态

git checkout+分支 切换到某一分支 

git checkout+文件名 把.git目录下的文件复制一份到当前目录下，就是说会把暂存区（git add后的 staging area）中的文件那来一份覆盖一当前工作目录下的同名文件。<font color="red">到底是git add后的还是git commit后？</font>

```shell
git checkout HEAD~2 .
git checkout HEAD~2 xxx.xxx		//采用距离现在的前两个版本的文件来覆盖当前文件
```

## 15.撤销修改

1.没add前

```shell
 git checkout -- readme.txt //把readme.txt文件在工作区的修改全部撤销。
```

2.add后 commit前

此时修改提交到了暂存区，但是没有提交到分支（git commit提交到分支）

```shell
git reset HEAD readme.txt //git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区，HEAD表示最新版本。撤销commit
git checkout -- readme.txt //丢弃工作区的修改。
```

3.commit后

只能回退到某一版本

```shell
git reset --hard HEAD^ //HEAD表示当前版本，则HEAD^表示上一个版本，那么上上版本就是HEAD^^ 应该也可以加版本号
```

再回到最新版本

```shell
git reset --hard 1094a //这里不能用HEAD而必须使用 commit id ，因为最新版本在之前返回时已经被删除了，1094a就是最新版本的 commit id，可以在之前的代码中查到
```

## 16.远程仓库

