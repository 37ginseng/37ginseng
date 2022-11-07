初始化仓库: `git init`

查看仓库状态: `git status`

向暂存区添加文件: `git add 123.txt`

提交到本地库: `git commit` or `git commit -m`

查看提交日志: 

* 全部 `git log` 
* 简略信息 ` git log --pretty=short` 
* 特定文件 ` git log README.md`
* 文件改动 `git log -p`
* 特定文件改动 `git log -p readme.md`

查看(当前)分支: `git branch`

创建分支: `git checkout -b {分支名称}`,并切换过去

切换分支: `git checkout {分支名称}` , 

合并到当前分支: `git merge --no-ff  {分支名称}`

以图标形式查看分支: `git log --graph`

回溯版本:`git rest --hard {目标时间点的哈希值}`







