# Learning_R
R language learning record.

####  📝 这里记录了我学习R的一些历程
#### 2022/4/14日 第一次上传
##### 在push的时候错误push到了master分支
##### 解决方法：先将文件从github上master上pull回来然后switch 分支master到main，然后merge master和main，再push，之后删除master分支：
###### `git pull --rebase origin master`
###### `git switch main`
###### `git merge --no-ff master`
###### `git push -d origin master`
