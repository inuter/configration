# git 的使用

1. create a new repository on the command line
```sh
$ echo "# demo" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin git@github.com:inuter/demo.git
$ git push -u origin master
```

2. push an existing repository from the command line
```sh
$ git remote add origin git@github.com:inuter/demo.git
$ git push -u origin master
```
3. pull an existing repository from the command line
```sh
$ git pull origin master
```

命令 | 功能
----|----
|git init | 在本地的当前目录里初始化git仓库|
git status | 查看当前仓库的状态
git add -A | 增加目录中所有的文件到缓存区
git add file | 增加相应文件到缓存区
git commit -m "信息" | 将缓存区中更改提交到本地仓库
git log | 查看当前版本之前的提交记录
git reflog | 查看HEAD的变更记录，包括回退
git branch -b branch_name | 建立一个新的分支
git diff | 查看当前文件与缓存区文件的差异
git checkout -- file | 取消更改，将缓存区的文件提取覆盖当前文件
git reset --hard 版本号	| 回退到相应版本号，同样也可以回退到未来的版本号
git clean -xf | 删除当前目录中所有未追踪的文件