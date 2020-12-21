# Git 场景bug记录

1. Git和Jenkins配合的时候，user.name 不应该与 Jenkins 已经存在的账号同名，否则将会取已经存在的用户的邮件地址。造成邮件发送错误的问题。

2. git checkout 无法切换分支，
   原因： git config core.ignorecase true 忽略大小写，造成无法识别分支名称
   解决：  git config core.ignorecase false 区分大小写，即可正常切换