### Git

1. ### 创建版本管理库

   - ###### 创建目录: mkdir 文件夹名称<span style="color: red"> (请确保文件夹名称和路径不含中文)</span>

   - ###### 跳转到目录: cd 文件夹名称

   - ###### 获取文件夹路径: pwd

2. ### 初始化版本库 git init

   - ###### 弹出以下提示表示成功: Initialized empty Git repository in "文件夹路径"
   - ###### 会在目录下创建一个名为.git的隐藏目录

3. ### 添加文件: git add 文件名称

4. ### 提交文件: git commit 文件名称 -m "变更描述"

5. ### 查看状态: git status 

   - ###### 可以让我们时刻掌握仓库当前的状态

   - ![image-20220208164121235](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220208164121235.png)
   
6. ### 查看记录: git log

   - ###### 显示从最近到最远的提交日志

   - ###### 按Q回车退出

   - ![image-20220208165857017](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220208165857017.png)

7. ### 版本回退: git reset --hard commit_id(HEAD^)

   - ###### 可直接在--hard后填版本的编码

   - ###### 也可以用HEAD, 并追加^可以多回退一个版本 ^^指2个 HEAD~100指100个
   
   - ![image-20220209214239647](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220209214239647.png)
   
8. ### 记录每次命令: git reflog

   - ###### 可查看后根据需要来进行版本回退

   - ![image-20220209214431752](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220209214431752.png)

9. ### 工作区和暂存区

   1. ##### 工作区(Working Directory): 比如Learn-git-220208就是一个工作区

   2. ##### 版本库(Repository):

      - ###### 工作区内有一个隐藏文件夹.git 是git的版本库 

      - ###### 版本库中最重要的就是称为stage或index的暂存区, 还有Git为我们创建的第一个分支master, 以及指向master的第一个指针Head

      - ![image-20220209215458153](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220209215458153.png)

      - ###### 我们把文件往Git版本库里添加的时候，是分两步执行的：

         第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

         第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支

         因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改

         ###### <span style="color:red">可以简单理解为, 需要提交的文件修改通通放到暂存区, 然后一次性提交暂存区的所有修改</span>

10. ### 查看差异: git diff HEAD(Commit ID) --readme.txt(指定文件名称)

   - ![image-20220210212346053](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220210212346053.png)

   - ###### 可能会有No newline at end of file的提示 文档末尾加一个回车即可解决

11. ### 撤销修改: git checkout --指定文件名称

    - ![image-20220210215238979](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220210215238979.png)

    - ###### 输入git check --指定文件名称后, 未提交的更新被撤回

       - ###### 只撤回工作区中的更新

    - ###### 如果已经commit则用reset

    - ![image-20220210215322056](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220210215322056.png)

12. ### 删除文件

    - ###### 执行 rm 文件名称 会直接删除目录下的文件, 并非在暂存区或版本库中删除

    - ###### 当文件已经提交后, 执行rm删除文件的话, 通过`git status`可以查看到文件被删除的记录

    - ![image-20220210221421673](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220210221421673.png)

    - ###### 这个时候git已经知道我们删除了某个文件

       - ###### 如果确认要从版本库中删除 则执行命令`git rm 文件名称`再进行 `git commit`

       - ![image-20220210221741963](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220210221741963.png)

       - ###### 另一种情况是删错了, 则执行`git checkout -- 文件名称`撤销

       - ###### <span style="color: red">注意: 没有被提交到版本库就被删除的文件, 是无法恢复的,`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**</span>
    
13. ### 创建远程版本库(GitHub)

    1. ###### 执行 ssh-keygen -t rsa -C "youremail@example.com"

       - ###### 一路回车 使用默认配置即可

       - ###### 用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人

    2. ###### 登录GitHub, 打开用户设置, 找到SSH Key界面,

       - ###### 点击Add SHH Key 填写title, 在Key文本框中粘贴id_rsa.pub文件的内容

       - ![image-20220213214134026](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220213214134026.png)

       - ![image-20220213214218350](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220213214218350.png)

       - ###### 添加完成后即可看到自己的Key了
    
14. ### 添加远程库

    1. ###### 登录GitHub, 在右上角找到New repository(新建存储库)

       - ![image-20220213215745937](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220213215745937.png)   

    2. ###### 根据GitHub的提示，在本地的`git-learn-0209`仓库下运行命令

       - ###### `git remote add origin git@github.com:9486983/git-learn-0213.git`
    
       - ###### 执行后再依次执行GitHub提示的语句
    
       - ![image-20220213222807143](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220213222807143.png)
    
       - ###### 首次推送时会进行SSH验证的警告, 输入`yes`回车即可
    
15. ### 克隆远程库

    1. ###### git clone git@github.com:用户名称/库名称.git
    
16. ### 分支管理

    1. ###### 创建分支

       - ###### `git checkout -b 分支名称 `

       - ###### 加上`-b`表示创建并切换

       - ###### 也可以用`git switch 分支名称`切换分支

    2. ###### 查看分支

       - ###### git branch

       - ###### 带*号的表示当前分支

       - ![image-20220219153807563](D:\A_MyFile\git-learn-220208\image-20220219153807563.png)

       - g
