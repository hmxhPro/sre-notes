# 01day note and summary
[git](https://www.git-scm.com/book/zh/v2/)


note :git操纵的是快照流，如果下一个项目版本只改动了部分文件，git只记录改动的文件，而不是整个项目，原有未改动的文件不会复制，会使用软连接指向原有文件

question :如果在没有网络的情况下，我多次运行了git add . 但是没有push，但我又想回到其中一个版本，我该怎样操作？

answer:add .会覆盖，commit才会形成版本，所以commit可以回退，add .不行


git的三种状态
1.committed
2.staged
3.modified

