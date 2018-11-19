### 将文件放进git里(本地)
- 1. git add 文件名  (添加文件)
- 2. git commit -m '说明' (提交文件，-m 是提交说明的命令，commit 可以一次提交多个add的文件)
    - git status  查看命令结果 (如果文件改动了，可以看到是否改动)
    - git diff    查看具体怎么修改了文件
    - git log     查看提交版本的历史记录 （HEAD表示当前版本）
    - git reset --hard HEAD^（或者commit_id）  (HEAD^，HEAD表示当前版本，HEAD^表示上一个版本，HEAD^^表示上上个版本，类推。使用git reset回到某个版本之后，再用git log就只能看见这个版本之前的版本了，但是记住版本的版本号（前几位就行），可以回到这个版本未来的版本。)
    - git reflog  记录每一次命令，可以在这里查到往期所有的命令，也能找到未来的版本号

### 几个概念
- 工作区（working directory）：工作目录
- 版本库（Repository）：工作区内的隐藏目录 .git，内含有：
    - stage(index) 暂存区  git add实际是把文件添加进暂存区
    - master (自动创建的第一个分区) git commit 实际是吧暂存区内的所有内容提交到当前分支
    - HEAD (指向master的一个指针)