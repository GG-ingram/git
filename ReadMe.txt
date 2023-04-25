什么是版本控制？
就是记录文件内容的变化，以便将来查阅版本更新状况
版本控制最重要的就是控制文件的修改历史记录，
版本控制 就是记录你的文件的版本变化 git就是一个记录版本变化的工具
就是比如 论文的修改，第一次完成论文初稿，第二次在第一次的基础上进行修改得到论文2.0 从一到二就是版本的控制
版本控制工具
1、集中式版本控制工具
svn、cvs
什么是集中式版本控制工具？
只有一台主服务器、主服务器上存储了你们的主要代码
我们想要获取服务器上的代码需要连接服务器 pull下来 然后编写代码 编写完成后push上去
就是一台主服务器管理代码 多个客户端来连接你的主服务器
多个客户端使用同一份代码，为了避免代码的混乱，约定大家的代码都放在中央服务器上，无论谁对代码进行修改，都要去中央服务器进行修改、
这样保证了多个人修改的代码是同一份代码，这就是集中式版本控制工具

分布式版本控制工具
git是分布式版本控制工具
对于分布式来说已经没有什么中央服务器了
每台客户端就是自己的代码库，在自己的电脑上做版本控制工具
怎么保证代码的统一性？
分布式版本控制工具都有一个代码托管中心的，每个程序员的电脑就是一个版本控制工具，
每个程序员在自己电脑上编写代码，此时写出来版本1 然后推送push到远程服务器上（就是远程库）
此时别人就可以使用自己的电脑连接远程库把那个版本1 clone（赋值，克隆）一份到你的本地库，然后基于你自己的本地库做你自己的版本控制
然后你又可以对这个版本1进行修改，进而推出版本2 然后push远程库，以此类推

说白了每个程序员的电脑就是一台服务器，有一个中央服务器（远程库）专门管理大家所写的代码，每个人都可以连接这个远程库
把自己的代码往上面传（push），也可以连接远程库将代码clone（就是下载）到自己的本地版本控制工具上进行修改，修改结束后推送
到远程库（就是中央服务器）


代码托管中心的分类
1、局域网 GitLab
2、互联网 Git GitHub Gitee（国内版本的GitHub）


================
git的常用命令
1、设置用户签名 安装好git后只需要设置一次git的用户签名就够了 必须设置的 如果不设置 以后提交代码的时候 git会报错
    git config --global user.name 用户名
    签名的作用是为了区分不同的操作者
    这里设置的用户签名和将来要登录GitHub的用户账号毫无关系（或者其他代码托管中心）
    注意没有空格
    一般也要设置自己的邮箱
    git config --global user.email 邮箱名称
    如何证明用户签名设置好了？
2、初始化本地库
    git init
    初始化本地库是什么？
    就是使用git管理你的目录，要想使用git管理你的目录，首先你得让git获取获取这个目录的管理权，就是初始化
    如果你的目录还没有初始化，你的git就管理不了，就是你的git没有这个目录的权限，但是你要想使用你的git管理他，你必须
    初始化本地库
    初始化结束后有这样的返回信息
    Initialized empty Git repository in D:/Git_Space/git_demo/.git/
    说有一个空的git库
    git 的命令和linux是通用的
3、查看本地库的状态
    git status
    返回本地库的信息
    On branch master
    表示当前的本地库在master的分支里面 这里的master就是开始在安装的时候你让git觉得的git默认的分支的名字
    master指的是当前的分支
    No commits yet
    表示本地库还没有提交
    nothing to commit (create/copy files and use "git add" to track)
    空的库，这个库没有东西可以提交
    如果库里面有东西
    使用 git status
    Untracked files:
    //表示未被追踪的文件
      (use "git add <file>..." to include in what will be committed)
      //这里hello.txt 是被标红的 表示你还没有提交这个文件 这个文件只是存在在工作区
            hello.txt
    nothing added to commit but untracked files present (use "git add" to track)
    者表示有的东西没有提交
4、如何把本地的文件添加到暂存区？
    添加暂存区--就是git追踪文件的过程
    git add 你想要放入暂存区的文件名字
    比如 git add hello.txt
    warning: LF will be replaced by CRLF in hello.txt.
    The file will have its original line endings in your working directory
    你使用git add命令后，你的本地库没有东西了 这时候使用git status
    你的本地库就会显示
    On branch master
    No commits yet
    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
            new file:   hello.txt
    //这里表示你提交到暂存区了 hello.txt 原来是红色的现在变为绿色，表明git追踪到这个文件了
    注意这个时候文件只是存在在暂存区里面，这个暂存区里面的文件是可以删除掉的
    关键来了！！！
    git的工作机制
    工作区（就是你写代码的地方，初始代码存放的位置）--> 暂存区（临时存储你的代码） --> 本地库（你的代码提交到本地库，有历史版本了，你不能修改了）
    在工作区和暂存区你可以修改你的代码，但是在本地库你不可以修改了
    如果你想把这个暂存区里面的文件删除掉的话，不想让他存到本地库的话
    使用命令 git rm --cache 文件名称 就是把你暂存区的这个文件删除，把这个文件放回到你的工作区里面
    cache就是缓存的意思，原本你的暂存区就是一个缓存
    这个删除只是把你暂存区的这个文件放回到你的工作区
    ！！！！！！！！！！
    最开始的时候你使用git init 初始化你的Git_demo 这个项目目录，就是说你将目录的管理权限交给git了
    以后这个git-demo就是你的工作区
    在工作区的文件是没有被git追踪过的，

4、提交本地库
   首先git的工作流程
   1、工作区
   2、暂存区
   3、本地库
   现在工作区编写你的代码，代码书写完毕之后，提交到暂存区，然后在暂存区又提交到本地库
   怎么提交到本地库？
   将暂存区的文件提交到本地库形成自己的历史版本
   git commit -m "版本日志信息" 文件名称
   m就是message的意思
   如果你不写这个-m 他也会提示你
   成功返回如下信息
   warning: LF will be replaced by CRLF in hello.txt.
   The file will have its original line endings in your working directory
   [master (root-commit) a173780] commit first
    1 file changed, 13 insertions(+)
    create mode 100644 hello.txt
   a173780就是你的版本号
   一旦提交到本地库后
   执行git status
5、使用git reflog 应用日志信息 或者使用git log查看想想日志
    $ git reflog
    a173780 (HEAD -> master) HEAD@{0}: commit (initial): commit first
    Head 指向 master 这个分支 版本号是 a173780 这个版本号是简短的
    git是使用c写的
6、使用git log
    $   git log
    commit a1737809c5b956b0d83960d935ec6ad71b3f75c2 (HEAD -> master)
    Author: root <root@qq.com>
    Date:   Sat Apr 22 23:52:34 2023 +0800
    commit first
    a1737809c5b956b0d83960d935ec6ad71b3f75c2 是完整版的版本号

    在git里是按照行来维护文件的
    注意暂存区的文件也是可以被修改的

    只要你提交到本地库，就会有版本的历史记录，
    在本地库的文件也是能修改的
    本地库只是记录版本变化
    在本地库的文件可以直接被修改
    在工作区可以直接提交到本地库
    在暂存区也可以体提交到本地库
    暂存区就是存放代码的
    只要你还没有提交到远程库，那么你的代码都死可以直接被修改的，只是修改过后的文件没有被git追踪到而已
    git是使用c编写的，只要你提交到本地库
    就会有一个指针指向你的这个文件
    git

7、查看版本信息
    git log --查看详细的版本信息
    git reflog -- 查看精简版的版本信息
    把代码的版本回调
    命令
    git reset --hard 版本号
    就是将版本降低
    注意这里版本的内容是你降低版本的内容
    比如你将5版本的降低为4版本，这时候你代码的内容就是4版本的





8、git的分支操作
    分支的底层就是指针的引用，可以理解为副本（但实际上不是副本）
    服务器在公司里面分好几套，分开发环境测试环境生产环境
    客户使用的是线上服务器，如果线上服务器修改了或者别的程序员要开发这个环境，不可能在用户用的线上服务器上开发
    所以代码要多复制几个分支，然后一个分支让用户使用
    一个分支给程序员们使用
    程序员在他们使用的那个分支上书写额外添加的代码。书写完毕后将他们的代码添加到主线分支上
    在版本控制的过程中需要同时推进多个任务，可以为多个任务开辟多个分支，在开发分支的时候不会影响主线分支
    一个分支就相当于一个副本，多个分支就相当于多个副本
    分支的底层就是指针的引用
    分支的好处
        并行推进多个功能的开发
        在开发的过程中如果一个分支开发失败，不会对其他分支有任何的影响
        失败的分支删除重新开始即可
9、分支的命令
    1、查看分支 git branch -v
    $ git branch -v
    * master ab9ac4e 版本5
    2、创建分支
    git branch 分支名字
    $ git branch hot-fix

    在这之后查看分支
    $ git branch -v
      hot-fix ab9ac4e 版本5
    * master  ab9ac4e 版本5
    3、修改分支
    4、切换分支
    git checkout 分支名称
    $ git checkout hot-fix
    Switched to branch 'hot-fix'
    ingram@DESKTOP-CVD5APC MINGW64 /D/Git_Space/git_demo (hot-fix)
    这时候分支就切换了
    每个分支都有工作区 暂存区 和 本地库
    分支就相当于副本

    分支合并
    git merge 分支名称
    把指定的分支合并到当前分支上面
    这里把hot-fix这个 分支合并到master分支
    使用
    在master分支里面 使用 git merge hot-fix
    ingram@DESKTOP-CVD5APC MINGW64 /d/Git_Space/git_demo (master)
    $ git merge hot-fix
    Updating ab9ac4e..428ec1c
    Fast-forward
    hello.txt | 2 ++
    1 file changed, 2 insertions(+)


    代码冲突的问题
    冲突的原因?产生代码合并冲突的原因
    这里的冲突是指两个分支都对同一个文件进行修改，而上一节没有冲突是因为只对hot-fix分支修改，master没有修改
    代码报错
    $ git merge hot-fix
    Auto-merging hello.txt //自动合并 hello.txt
    CONFLICT (content): Merge conflict in hello.txt //在合并 hello.txt 时发生冲突
    Automatic merge failed; fix conflicts and then commit the result.
    ingram@DESKTOP-CVD5APC MINGW64 /d/Git_Space/git_demo (master|MERGING)
    (master|MERGING) 正在合并中
    此时查看本地库状态
    $  git status
    On branch master
    You have unmerged paths.
      (fix conflicts and run "git commit")
      (use "git merge --abort" to abort the merge)
    Changes to be committed:
            modified:   my.txt
    Unmerged paths:
      (use "git add <file>..." to mark resolution)
            both modified:   hello.txt

    为什么会产生冲突？
    原因时你两个分支都对一个文件进行编写，修改，在1分支里面对x.txt写代码 在2分支里面也对2分支的x.txt 写代码，然后合并，然而，
    git不知道使用哪个去覆盖哪个，是使用1的x.txt去覆盖2的x.txt 还是使用2的去覆盖1的？git不能决定
    所以要我们去自己合并
    git帮我们指出冲突的地方
    <<<<<<< HEAD
    master test
    =======
    master test2
    >>>>>>> hot-fix

    这里git指出 在当前分支的 代码 master test 与 hot-fix分支 的代码master test2起冲突了
    修改完毕后 添加暂存区
    然后提交
    注意
    提交 时使用 git commit -m "日志信息"
    不能加文件名了
    合并之后，这里比如在master分支合并hot-fix分支，master分支代码变化，但是hot-fix分支的没有变化
    冲突的出现是因为你两个分支都对一个文件进行修改了


    git合并分支底层使用的也就是指针

    //养成习惯 修改完毕 添加缓存区 然后没有问题 提交本地库
10、git 团队协作
    如何利用git做团队协作？
    使用远程托管中心
    1、团队内协作
    将本地库的代码push（推送）到代码托管中心 开发人员依据自己的需求clone（下载）下来到自己的本地库
    开发人员依据clone下来的代码进行二次修改得到版本2x 然后又push到远程托管中心，当然，你往远程库push代码需要权限，不然乱套了
    第一个开发人员将自己的代码推送到远程库，之后这个代码被别的开发人员升级了，此时第一个开发人员将代码pull下来到自己的本地库，就会更行自己本地库的代码
    本地库的代码
    pull和clone是不一样的 pull拉去下来是会更新自己的本地库的（前提是你本地库要有东西）
    2、跨团队协作

    不同团队都有自己的远程库
    甲团队有自己的远程库，乙团队有自己的远程库
    甲团队需要乙团队帮甲做一些代码的维护
    这时乙团队就会执行一个操作 就是fork操作，就是叉过来，将甲的远程库的项目a fork到自己的仓库中 这样乙团队就有甲的项目
    然后乙团队就可以对甲的项目进行修改和操作了
    之后乙团队将修改后的代码发布到自己的远程库，乙团队通过 pull request（拉取请求）将拉去请求告诉甲团队 这个拉取请求就是告诉你项目好了，赶紧拉走
    pull request 就是发布拉取信息，通知别人来我的库拉取项目
    在拉取之前还要审核 一旦审核通过就会merge 将项目合并


    ==========================================================================================================================

    一般远程库的名字和本地库是一样的

    创建远程库别名 链接太长了 不好记忆
    git remote -v 查看当前所有远程地址别名
    ori     https://github.com/GG-ingram/git-demo.git (fetch)
    ori     https://github.com/GG-ingram/git-demo.git (push)
    这里别名既可以推送也可以拉取
    push pull clone 都可以使用这个别名
    git remote add 远程地址
    将本地库的分支推送到远程库里面去
    git push 别名 分支
    出现以下结果
    $ git push ori hot-fix
    Select an authentication method for 'https://github.com/':
      1. Web browser (default)
      2. Personal access token
    option (enter for default): 1
    info: please complete authentication in your browser...
    Enumerating objects: 24, done.
    Counting objects: 100% (24/24), done.
    Delta compression using up to 16 threads
    Compressing objects: 100% (20/20), done.
    Writing objects: 100% (24/24), 2.11 KiB | 719.00 KiB/s, done.
    Total 24 (delta 4), reused 0 (delta 0), pack-reused 0
    remote: Resolving deltas: 100% (4/4), done.
    To https://github.com/GG-ingram/git-demo.git
     * [new branch]      hot-fix -> hot-fix


    拉取命令
    顾名思义就是把远程库的代码拉取到本地库
    推送和拉取是一样的
    拉取过来的结果和远程库的是同步的
    git pull url 分支名称
    输出结果
    这段输出是一个git命令git pull的执行结果，表示从远程仓库上（git-demo）拉取了最新版本的代码，并对代码库进行了更新。这里面包含了以下内容：
    remote: Enumerating objects: 5, done. 表示正在枚举来源仓库中的对象。
    remote: Counting objects: 100% (5/5), done. 表示已统计引入对象数量。
    remote: Compressing objects: 100% (3/3), done. 表示正在压缩引入的对象。
    remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 表示引入3个原始对象，其中1个为增量。
    Unpacking objects: 100% (3/3), 710 bytes | 101.00 KiB/s, done. 表示成功解包所有对象。
    From https://github.com/GG-ingram/git-demo 表示数据提取自该地址。
    * branch            master     -> FETCH_HEAD 表示本地的master分支同步完毕，并将远程的master分支合并到了FETCH_HEAD中。
    056aedc..d4b8b55  master     -> ori/master 表示在本地的master分支上，从commit ID 056aedc 更新到了 commit ID d4b8b55。
    Updating 056aedc..d4b8b55 表示正在更新 commit.
    Fast-forward hello.txt | 1 + 表示在当前本地的分支上，从GitHub取回最新的提交历史记录，并且将这些修改添加到master分支中去。也就是说你github上修改的hello文件现在已同步到本地仓库的hello.txt文件中，其中 1 insertion(+) 表示,hello.txt`文件添加了一行。


    git 克隆
    git clone 远程地址
    克隆结果就是初始化本地库
    使用git的clone命令之前需要初始化本地库吗？
    不需要。git clone 命令用于将远程 Git 代码库克隆到本地机器上，它自动将所有信息（包括版本控制器、问题列表、历史记录等）从指定的远程存储库中复制到本地文件系统中。
    在使用git clone命令时，Git会自动为您创建一个新的本地目录，其中包含了克隆源存储库中的所有数据和状态，并将其作为一个新的Git存储库进行初始化。因此，不需要手动执行 git init 命令来对其进行初始化。
    以下是一个典型的 git clone 操作的示例
    $ git clone https://github.com/username/repo.git
    Cloning into 'repo'...
    remote: Counting objects: 10, done.
    remote: Compressing objects: 100% (8/8), done.
    remote: Total 10 (delta 1), reused 8 (delta 0), pack-reused 0
    Receiving objects: 100% (10/10), done.
    Resolving deltas: 100% (1/1), done.
    克隆会做的事情:
    1、初始化本地库
    2、拉起代码
    3、给这个库其别名
    克隆代码是不需要登录的




团队内协作
    1、邀请合作者



