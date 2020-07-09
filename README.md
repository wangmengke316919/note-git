# Git

## 入门

git命令行操作跟Linux一样

### 1 安装

1. Use git from git bash only..., 其他默认下一步
2. 查看环境变量配置, 没有则手动配置, path: E:\programs\Git\bin
3. 配置git, 桌面右键git bash..., 配置用户名和邮箱

    ```git
    git config --global user.name hua
    git config --global user.email "2827890646@qq.com"
    ```

该配置文件在本地计算机c:\user\用户\.gitconfig

### 2 git status, git commit等中文信息乱码问题

```git
git config --global gui.encoding utf-8
git config --global i18n.commitencoding utf-8
git config --global core.quotepath false
git config --global svn.pathnameecoding utf-8
```

### 3 本地git与远程github保持登录联通

git 的远程仓库托管网站目前就[github](https://github.com)一个常用

为了在本地和远程仓库之间进行操作, 可采取免密钥登录,配置ssh. 先在本地配置, 然后把公钥发送给远程仓库github.

1. 在本地git命令行中输入:

    ```git
    ssh-keygen -t rsa -C 2827890646@qq.com
    ```

2. 然后一直回车, 出现下图则表示成功

    ![03-01](./img/03-01.jpg)

3. 发送给远程github

    1. github -> settings -> SSH and ... -> New SSH -> title & key

        ![03-02](./img/03-02.jpg)

    2. 复制本地公钥到key中, 删掉最后的回车占位符
    3. 如果本地和远程成功通信, 则在本地./ssh目录中自动生成**known-hosts**文件
    4. 测试本地仓库与远程仓库的登录连通性, git命令行:

        ```git
        ssh -T git@github.com
        ```

### 3 本地创建git项目于远程项目进行关联

1. 先创建一个目录demo
2. 进入该目录,鼠标右键点击git bash..., 打开git命令端, 输入**git init**, 会自动在demo目录下生成**.git**目录(该目录是隐藏的).
3. github上创建一个Repository.

    ![04-01](./img/04-01.jpg)

4. 第一次发布项目(本地 -> 远程)

    ```git
    git init
    git add . // 文件 -> 暂存区, "." 表示当前目录下的所有文件提交暂存区
    git commit -m "第一次提交"  // 暂存区 -> 本地分支(默认为master)
    git remote add origin <远程项目所在的ssh地址(或http协议地址)>
    git push -u origin master // 本地分支 -> 远程项目
    ```

5. 第一次下载项目(远程 -> 本地)

    本地创建一个目录, 进入该目录, 打开git命令终端, 输入下面命令:

    ```git
    git clone git@github.com:yanse/mygitdemo.git
    ```

6. 非第一次提交(本地 -> 远程)

    ```git
    git add .
    git commit -m "第二次提交"
    git push origin master // 注意: 这里去掉了 -u (其实可以简写成git push)
    ```

7. 更新(远程 -> 本地)

    1. 在远程项目中修改文件.

        ![04-02](./img/04-02.jpg)

    2. 本地项目中, git命令行输入**git pull**即可更新.
