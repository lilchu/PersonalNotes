### 将文件放进git里，三步
- 1. git add 文件名  (添加文件)
- 2. git commit -m '说明' (提交文件，-m 是提交说明的命令，commit 可以一次提交多个add的文件)
    - git status  查看命令结果 (如果文件改动了，可以看到是否改动)
    - git diff    查看具体怎么修改了文件
    - git log     查看提交版本的历史记录 （HEAD表示当前版本）
    - git reset --hard HEAD^  (HEAD^，HEAD表示当前版本，HEAD^表示上一个版本，HEAD^^表示上上个版本，类推)
- 3. 修改测试

