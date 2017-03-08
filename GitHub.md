##github

###本地操作
- 首先在工作目录git bush 输入`git init`命令初始化,让git接管该目录
- 修改文件之后输入`git add 文件名`将文件推送到缓存区;批量推送使用`git add *`
- 将暂存区的文件提交到master使用`git commit -m '文件描述'`命令;
- git将为这个版本的文件指派版本ID,这个ID是日后版本控制的依据;
- 查看状态使用`git status`;
- 查看文件差异使用`git diff 文件名`查看工作目录文件改动后与master的差异
- `git diff 文件名1 文件名2`查看两个文件之间的差异

###删除与恢复
- 使用`git rm 文件名`删除指定文件
- 使用`git checkout 文件名`恢复被删除的文件(实际是从版本库中恢复)


###版本控制
- 使用`git log`查看所有commit历史,使用`git log --pretty=oneline`单行显示信息,包括版本ID;
- 使用 `git reset --hard 参数`在版本间跳转;
	--hard的参数:
	- `HEAD`:HEAD总是指向当前版本,如果要回退一个版本在版本后加`^`,也可以加`~n`,回退当前版本之前n个版本;
	- 参数可以是各版本的版本ID,使用`git log`或者`git reflog`,`reflog`只会显示版本ID前几位,但不用担心,git依然能够找到正确的版本;


###pull&push
* 第一次需要先关联上远程仓库: `git remote add origin url(远程仓库的地址)`
* 推送之前先同步代码，将远程最新版本拉到本地: `git pull origin master`
* 将本地版本区(HEAD)的更新推送到远程仓库 : `git push origin master`
* 提示输入username:xty2017a
* 提示输入password:********