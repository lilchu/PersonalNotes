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
- git 跟踪并管理的是修改，而不是文件，这是git比其他版本控制软件设计得更加优秀的原因之一
- git checkout -- filename 可以丢弃工作区的修改，这句代码的含义是把filename在工作区的修改全部撤销，有两种情况:
    - 一是filename自修改后还没有放进暂存区（没有add），现在撤销修改就和版本库内的文件一模一样了
    - 二是filename已经添加到暂存区，又作了修改，现在撤销修改就回到添加到暂存区后的状态
    - 总之就是回到最近一次commit或者add的状态，最近一次是commit就是commit状态，是add就是add状态
- git reset HEAD <filename> 可以把暂存区的修改撤销掉（unstage）,重新放回到工作区
- bash里返回 changes not staged for commit，就是文件在工作区修改了，但是没有add进暂存区
- bash里返回 changes to be committed, 就是文件在工作区修改了，且放入了暂存区，还没有提交进入版本库
- git checkout -- <filename> 可以丢弃工作区的修改
- 删除文件
    - 工作区可以用rm直接删除，但是暂存区和版本库还在，可以用git status查看状态
    - 从版本库删除文件，用git rm <filename>, 并且git commit

### 远程仓库（使用github）
- 1. 本地仓库与远程仓库之间是用ssh加密的，需要创建SSH KEY，看看用户主目录下有没有.ssh目录，再看看这个目录下有没有id_rsa,id_rsa.pub这两个文件，如果没有则打开shell（windows上是git bash），创建ssh key: ssh-keygen -t rsa -C "lilzhuchunwu@gmail.com" (无需设置密码，一路回车)  （ssh存储位置在/c/Users/zhuchunwu/.ssh/id_rsa）
- 2. 登录github， 打开Account settings - SSH keys 页面，点击Add SSH KEY, 填上Title，在文本框里粘贴 id_rsa.pub文件的内容
- 3. github上create new repository "PersonalNotes"
- 4. 在本地的working directory下运行： git remote add origin git@github.com:lilchu/PersonalNotes (远程库的名字就叫origin，这是git默认的叫法,使用这个命令不会遇到输入账号密码的问题，这是ssh登陆) 
- 5. 将本地库的所有内容推送到远程库上： git push -u origin master(实际是将当前分支master推送到远程，由于远程库为空，第一次推送时加上了-u参数，git不仅会将本地的master分支推送到远程的master分支上，还会将二者关联起来，以后再推送和拉取时会简化命令)
- 6. 可能会遇到（ failed to push some refs to ）问题，得先拉取使用git pull origin master 再上传 git push -u origin master

### 克隆
    - 先在github上创建一个远程库，然后使用 git clone git@github.com:lilchu/example,多人开发就各自克隆一份就行了。
    - git支持多种命令（http https等），但是ssh支持的原生git协议速度最快

### 分支管理
    - 分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。
    - 1. 创建 dev 分支： git checkout -b dev (-b 表示创建并切换,相当于git branch dev 和 git checkout dev)
    - 2. 用git branch 命令查看当前分支，当前分支会有个*号
    - 3. git checkout master 会切换到master分支上，但是dev上的数据就不显示了
    - 4. 使用git merge dev 将dev分支上的数据合并到master上（git merge用于合并分支到当前分支，要注意当前分支是什么，默认和并方式为fast-forward）
    - 5. 使用git branch -d dev 删除分支