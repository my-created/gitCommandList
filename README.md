# 自己总结的git命令列表

## 日常 Git 操作

1. 在项目目录中右击鼠标，选择 `Git Bash Here`

2. `git pull` 拉取当前分支到本地，并且合并。

3. 如果在dev分支上执行4。

4. `git checkout -b [分支名]（如add_user）` 创建分支，并切换到这个分支。

5. 执行2，开始开发。（注意，不能在dev上开发，新建自己分支开发，命令4）

6. 随时执行 7,8,9

7. `git status` 查看当前版本库状态

8. `git add . ` 在项目根目录下执行，添加所有不在版本库的文件到暂存区，如果想添加某一个，可以直接添加文件路径 `git add xxx.xxx`。

9. `git commit -m "[操作] [信息]"`  提交所有暂存区文件到本地版本库。

10. `git push origin [当前分支名]`  推送本地版本库到远程版本库。

11. 一天工作结束，必须有一次 `7,8,9,10` 操作。

12. 功能完成后操作 `13` 或者 `14` 。

13. 一个功能完成后，或者说功能上线，执行 `10` ，并到 `gitlab` 页面，选择你当前的分支，点击页面右侧的创建合并请求，`Assignee` 选择你的领导， `Target branch` 选择 `dev` ，然后点击 `submit` 。

14. 通过通讯工具 `QQ,微信，钉钉` 等，通知上级审查，合并功能，通知格式 [xx库] [xx分支] [xx功能]已完成或已提交

15. `git merge --no-ff dev` 保留commit历史合并dev到当前分支

16. `git push origin --delete <branchName>` 删除远程分支

17. `git fetch -p` 删除没有远程分支的本地分支

18. `git tag -a v1.4 -m 'my version 1.4'` 含标注的标签

19. `git tag v1.5` 轻量级标签

20. `git tag -a v1.2 9fceb02` 给某个commit打tag

21. `git log --pretty=oneline` 单行显示log

22. `git diff --name-status  master dev` 对比dev 相对于 master的文件更改状况，显示文件列表

23. `git diff --name-only master dev | xargs tar -czvf update.tar.gz` 对比dev 到master的改变，并打包压缩。

24. `xargs -a up.log  tar -czvf  updata.tar.gz` 也可分开执行，导出改变的文件列表，剔除不需要打包的，然后通过 `xargs -a file` 导入并打包。

25. `git reflog` 显示所有操作的log（commit，checkout，等等其他的还没验证）

26. `git reset --hard 56a23`  硬重设： HEAD 到指定commit。效果是这个commit之后的更改都没了，工作区是干净的。其实操作就是删除了当前commit之后的commit。

27. `git reset --soft 56a23`  软重设:  HEAD 到指定commit。效果是这个commit之后的更改都当做 change list 显示了。其实操作就是重设HEAD，不删除commit。

28. `git revert` 还没搞懂，不记录，留个位置。

29. `git stash`  贮藏，想在分支之间切换，但是又有半成品的或者不想提交的修改，使用它。

>效果：工作区干净了，贮藏区有东西了。被缓存的文件有：跟踪的更改。不会缓存：未跟踪的文件。

>注意 `git stash` 只保存在本地，不会因为push而被推到线上。

30. `git stash save "提示文字"` 带提示文本的贮藏功能，推荐使用这种贮藏，免的忘记。

31. `git stash pop` 弹出第一个贮藏到工作区。效果：stash的第一个变成了当前分支的 change list 。

32. `git stash apply` 根据先后顺序依次覆盖所有贮藏到工作区，并且不删除贮藏。

33. `git stash list` 显示所有的贮藏。

34. `git stash drop stash@{0}` 删除第1个贮藏。

35. `git stash show` 查看贮藏和当前分支的 `diff` 情况。显示 `diff` 的文件列表。

36. `git stash show -p` 或者 `-patch` 查看贮藏和当前分支的 diff 情况。显示diff的文件内容。

37. `git stash branch testchanges` 根据贮藏开始的commit创建新分支。当现存分支不能正常导出贮藏的时候，使用它。

rebase vs. merge // 还未彻底搞清楚
38. `git pull --rebase || git rebase` 效果：合并远程分支到本地分支，分支记录保持一条直线。

39. `git pull` 效果：合并远程分支到本地分支，分支记录

merge vs. merge --no-ff
40. `git merge` 是不保留 `commit` 并新建 `merge commit`

41. `git merge --no-ff` 保留 `commit` 并新建 `merge commit`

42. `git merge --abort` 回到 `merge` 之前的状态，这个命令不总是成功。

版本回退
43. `git reset --hard` 版本号 ，下面俩个是这个的应用

绿字变红字(撤销add)
`git reset HEAD`

红字变无 (撤销没add修改)
`git checkout -- 文件`

当前分支有修改，但是不能在当前分支提交，直接切换到对应分支提交就行。

`git config --global log.date iso` 设置git log 时间显示格式为ISO标准时间格式。

`git diff branch1 branch2 --stat`   //显示出所有有差异的文件列表

`git diff branch1 branch2 文件名(带路径)`   //显示指定文件的详细差异

`git diff branch1 branch2`                 //显示出所有有差异的文件的详细差异
