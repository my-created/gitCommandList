# git 命令列表

## 创建 git 项目必备设置

1. `git config --global core.ignorecase false` 设置版本库区分大小写

2. `git config --global log.date iso` 设置 `git log` 时间显示格式为ISO标准时间格式。

## 日常操作

1. `git pull` 拉取当前分支到本地，并且合并

2. `git merge dev` 合并最新的开发分支 `dev`，保持自己分支的进度，避免最后合并时有太多冲突

3. `git checkout -b [分支名]（如add_user）` 创建分支，并切换到这个分支

4. `git status` 查看当前版本库状态

5. `git add . | git add xxx` 添加文件到暂存区，`.` 当前文件夹下所有文件 `xxx` 是具体文件路径

6. `git commit -m "[操作] [信息]"`  提交所有暂存区文件到本地版本库

7. `git push origin [当前分支名]`  推送本地版本库到远程版本库

8. 一天工作结束，必须有一次 `4,5,6,7` 操作

9. 功能完成后操作 `11` 或者 `14`

10. gitlab 这种 `web` 端管理软件管理时，一个功能完成后，或者说功能上线，执行 `7`，并到 `gitlab` 页面，选择你当前的分支，点击页面右侧的创建合并请求，`Assignee` 选择你的领导，`Target branch` 选择 `dev`，然后点击 `submit`，非 web 端软件管理，直接 `10`，找上级合并

## 高级操作

12. `git push origin --delete <branchName>` 删除远程分支

13. `git fetch -p` 删除没有远程分支的本地分支

14. `git tag -a v1.4 -m 'my version 1.4'` 含标注的标签

15. `git tag v1.5` 轻量级标签

16. `git tag -a v1.2 9fceb02` 给某个 `commit` 打 `tag`

17. `git log --pretty=oneline` 单行显示 `log`

18. `git diff --name-status  master dev` 对比 `dev` 相对于 `master` 的文件更改状况，显示文件列表

19. `git diff --name-only master dev | xargs tar -czvf update.tar.gz` 对比 `dev` 到 `master` 的改变，并打包压缩。

20. `xargs -a up.log  tar -czvf  updata.tar.gz` 也可分开执行，导出改变的文件列表，剔除不需要打包的，然后通过 `xargs -a file` 导入并打包。

21. `git stash`  贮藏，想在分支之间切换，但是又有半成品的或者不想提交的修改，使用它。效果：工作区干净了，贮藏区有东西了。被缓存的文件有：跟踪的更改。不会缓存：未跟踪的文件。 >>注意 `git stash` 只保存在本地，不会因为 `push` 而被推到线上。

22. `git stash save "提示文字"` 带提示文本的贮藏功能，推荐使用这种贮藏，免的忘记。

23. `git stash pop` 弹出第一个贮藏到工作区。效果：`stash` 的第一个变成了当前分支的 `change list`。

24. `git stash apply` 根据先后顺序依次覆盖所有贮藏到工作区，并且不删除贮藏。

25. `git stash list` 显示所有的贮藏。

26. `git stash drop stash@{0}` 删除第1个贮藏。

27. `git stash show` 查看贮藏和当前分支的 `diff` 情况。显示 `diff` 的文件列表。

28. `git stash show -p` 或者 `-patch` 查看贮藏和当前分支的 `diff` 情况。显示 `diff` 的文件内容。

29. `git stash branch testchanges` 根据贮藏开始的 `commit` 创建新分支。当现存分支不能正常导出贮藏的时候，使用它。

30. `git pull --rebase || git rebase` 效果：合并远程分支到本地分支，分支记录保持一条直线。

31. `git pull` 效果：合并远程分支到本地分支，分支记录。

32. `git merge` 是不保留 `commit` 并新建 `merge commit`

33. `git merge --no-ff dev` 保留 `commit` 历史，并新建 `merge commit`，然后合并 `dev` 到当前分支

34. `git merge --abort` 回到 `merge` 之前的状态，这个命令不总是成功。

## 版本回退

35. `git revert` 还没搞懂，不记录，留个位置。

36. `git reset --hard` 版本号 ，下面俩个是这个的应用。

37. `git reset --hard 56a23`  硬重设： `HEAD` 到指定 `commit`。效果是这个 `commit` 之后的更改都没了，工作区是干净的。其实操作就是删除了当前 `commit` 之后的 `commit`。

38. `git reset --soft 56a23`  软重设:  `HEAD` 到指定 `commit`。效果是这个 `commit` 之后的更改都当做 `change list` 显示了。其实操作就是重设 `HEAD`，`不删除commit`。

39. `git reset HEAD` 绿字变红字(撤销add)

40. `git checkout -- 文件` 红字变无 (撤销没add修改)

41. `git checkout [分支]` 切换分支，修改未 `add` 使用 `checkout` 切换分支后，修改会变到对应分支

43. `git diff branch1 branch2 --stat` 显示出所有有差异的文件列表

44. `git diff branch1 branch2 文件名(带路径)` 显示指定文件的详细差异

45. `git diff branch1 branch2` 显示出所有有差异的文件的详细差异

46. `git reflog` 显示所有操作的 `log`（commit，checkout，等等其他的还没验证）
