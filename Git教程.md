# Git教程

## 	Git简介

​			Git的诞生

1. Git可以记录每次文件的改动

2. Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！Linus一直痛恨的CVS及SVN都是集中式的版本控制系统，而Git是分布式版本控制系统。

   ​	集中式VS分布式

   1. 集中式

      集中式版本控制系统，版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。

      - 缺点：

        集中式版本控制系统最大的毛病就是必须联网才能工作

   2. 分布式

      集中式和分布式版本控制系统的区别：

      1. 分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。
      2. 和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了。
      3. 在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

      ## 	创建版本库

      版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

      1. 创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：

      ```
      $ mkdir learngit
      $ cd learngit
      $ pwd
      /Users/michael/learngit
      ```

      `pwd`命令用于显示当前目录。在我的Mac上，这个仓库位于`/Users/michael/learngit`。

      #####  如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。

      2. 通过`git init`命令把这个目录变成Git可以管理的仓库：

         ```
         $ git init
         Initialized empty Git repository in /Users/michael/learngit/.git/
         ```

      瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

      如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

      ​	也不一定必须在空目录下创建Git仓库，选择一个已经有东西的目录也是可以的。

      

      小结：初始化一个Git仓库，使用`git init`命令。

      添加文件到Git仓库，分两步：

      1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
      2. 使用命令`git commit -m <message>`，完成。

      

      

      

      ## 远程仓库

      你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的

      1. 创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

         ```
         $ ssh-keygen -t rsa -C "youremail@example.com"
         ```

         你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

         如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

      2. 登陆GitHub，打开“Account settings”，“SSH Keys”页面：

         点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

         ![github-addkey-1](https://www.liaoxuefeng.com/files/attachments/919021379029408/0)

         点“Add Key”，你就应该看到已经添加的Key：

         ![github-addkey-2](https://www.liaoxuefeng.com/files/attachments/919021395420160/0)

         思考：

         为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

         GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

         最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。

         ### 添加远程库

      ​		已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。

      - 登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

        ![github-create-repo-1](https://www.liaoxuefeng.com/files/attachments/919021631860000/0)

        - 在Repository name填入`Tasks2`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：

        ![github-create-repo-2](https://www.liaoxuefeng.com/files/attachments/919021652277920/0)

        目前，在GitHub上的这个`Tasks2`仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

        - 现在，我们根据GitHub的提示，在本地的`Tasks2`仓库下运行命令：

        ```
        $ git remote add origin git@github.com:DDDSSSro123/Tasks2.git
        ```

      添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

      - 就可以把本地库的所有内容推送到远程库上：

        ```
        $ git push -u origin master
        Counting objects: 20, done.
        Delta compression using up to 4 threads.
        Compressing objects: 100% (15/15), done.
        Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
        Total 20 (delta 5), reused 0 (delta 0)
        remote: Resolving deltas: 100% (5/5), done.
        To github.com:michaelliao/learngit.git
         * [new branch]      master -> master
        Branch 'master' set up to track remote branch 'master' from 'origin'.
        ```

      

      把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

      由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

      推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：

      ![github-repo](https://www.liaoxuefeng.com/files/attachments/919021675995552/0)

      从现在起，只要本地作了提交，就可以通过命令：

      ```
      $ git push origin master
      ```

      把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

      ### SSH警告

      当你第一次使用Git的`clone`或者`push`命令连接GitHub时，会得到一个警告：

      ```
      The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
      RSA key fingerprint is xx.xx.xx.xx.xx.
      Are you sure you want to continue connecting (yes/no)?
      ```

      这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入`yes`回车即可。

      Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

      ```
      Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
      ```

      这个警告只会出现一次，后面的操作就不会有任何警告了。

      如果你实在担心有人冒充GitHub服务器，输入`yes`前可以对照[GitHub的RSA Key的指纹信息](https://help.github.com/articles/what-are-github-s-ssh-key-fingerprints/)是否与SSH连接给出的一致。

      ### 删除远程库

      如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息：

      ```
      $ git remote -v
      origin  git@github.com:michaelliao/learn-git.git (fetch)
      origin  git@github.com:michaelliao/learn-git.git (push)
      ```

      然后，根据名字删除，比如删除`origin`：

      ```
      $ git remote rm origin
      ```

      此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

      ### 小结

      要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

      关联一个远程库时必须给远程库指定一个名字，`origin`是默认习惯命名；

      关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

      此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

      分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

      

      

      ## 	从远程库克隆

      上次我们讲了先有本地库，后有远程库的时候，如何关联远程库。

      现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

      首先，登陆GitHub，创建一个新的仓库，名字叫`Tasks`：

      ![github-init-repo](https://www.liaoxuefeng.com/files/attachments/919021808263616/0)

      我们勾选`Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件：

      ![github-init-repo-2](https://www.liaoxuefeng.com/files/attachments/919021836828288/0)

      现在，远程库已经准备好了，下一步是用命令`git clone`克隆一个本地库：

      ```
      $ git clone git@github.com:DDDSSSro123/Tasks.git
      Cloning into 'Tasks'...
      remote: Counting objects: 3, done.
      remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
      Receiving objects: 100% (3/3), done.
      ```

      注意把Git库的地址换成你自己的，然后进入`lxr`目录看看，已经有`README.md`文件了：

      ```
      $ cd T
      $ ls
      README.md
      ```

      ​			

      

​			

