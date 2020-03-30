# Git 场景bug记录

1. Git和Jenkins配合的时候，user.name 不应该与 Jenkins 已经存在的账号同名，否则将会取已经存在的用户的邮件地址。造成邮件发送错误的问题。
