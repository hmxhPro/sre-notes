# 01day note and summary
[git](https://www.git-scm.com/book/zh/v2/)

安装Git之后需要配置用户名和邮箱

eg:
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com

note :git操纵的是快照流，如果下一个项目版本只改动了部分文件，git只记录改动的文件，而不是整个项目，原有未改动的文件不会复制，会使用软连接指向原有文件

question :如果在没有网络的情况下，我多次运行了git add . 但是没有push，但我又想回到其中一个版本，我该怎样操作？

answer:add .会覆盖，commit才会形成版本，所以commit可以回退，add .不行


git的三种状态
1.committed
2.staged
3.modified

工作流 工作区(修改文件的区域)-> 暂存区(选择性的暂存) -> 提交区(commit形成版本,此时可以回退)

question:如果我在不同的目录执行了add .，会不会出错？
answer:不会，只要属于同一个git仓库，但是git init 会初始化一个新的仓库，所以不能在不同的目录执行git init


question: 如果我已经使用git追踪了一个文件，然后又将其添加到了.gitignore文件中，会发生什么情况？
answer: 已经被 Git 追踪（tracked）的文件，即使后来写进 .gitignore，Git 也不会忽略它