> 安装Node.js

[点击这里](https://nodejs.org/zh-cn/download/)
访问官网，下载你电脑相应版本，默认安装就可以了。
> 安装 Git

[点击这里](https://git-scm.com/download/win)访问官网，下载你电脑相应版本，默认安装即可。
> 检验Git是否安装成功

按下 Win+R 键打开运行窗口,输入 cmd ，然后输入以下命令，有相应版本号显示就安装成功了，若不显示或者报错可以卸载软件重新安装，此外若安装成功，在桌面右键鼠标，可以看到菜单里多了 Git GUI Here 和 Git Bash Here两个选项，第一个是图形界面的Git操作，另一个是命令行。
```
1| $ git --version
2| $ node -v
3| $ npm -v
```
> 安装Hexo

选择一个磁盘，新建一个文件夹，自己重命名文件夹，博客相关文件将储存在你创建文件夹下，在该文件夹下右键鼠标，点击 Git Bash Here，输入以下 npm 命令即可安装，第一个命令表示安装 hexo，第二个命令表示安装 hexo 部署到 git page 的 deployer，等待安装完成。
```
1| $ npm install hexo-cli -g
2| $ npm install hexo-deployer-git --save
```
> 初始化配置Hexo

在刚才新建的文件夹里面再次新建一个 Hexo文件夹，进入该 Hexo 文件夹右键鼠标，点击 Git Bash Here，输入以下命令，等待安装完成。
```
1| $ hexo init
```
Hexo 安装完成后，将会在指定文件夹中新建所需要的文件。
> 本地查看博客效果

执行以下命令，执行完即可登录 http://localhost:4000/ 查看效果
```
1| $ hexo generate
2| $ hexo server
```
显示以下信息说明操作成功：
```
INFO Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```
> 将博客部署到 Github Pages 上

到目前为止，我们的本地博客就成功搭建了，但是现在我们只能通过本地连接查看博客，我们要做的是让其他人也能够访问我们的博客，这就需要我们将博客部署到Github Pages上。
> 注册 Github 账户

[点击这里](https://github.com/)访问 Github 官网，点击 Sign Up 注册账户。
> 创建项目代码库

点击 New repository 开始创建，步骤及注意事项见下图：
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/1.png)
> 配置 SSH 密钥

只有配置好 SSH 密钥后，我们才可以通过 git 操作实现本地代码库与 Github 代码库同步，在你第一次新建的文件夹里面 Git Bash Here 输入以下命令：
```
1| $ ssh-keygen -t rsa -C "your email@example.com"
2| //引号里面填写你的邮箱地址，比如我的是chenzhilin18@outlook.com
```
之后会出现：
```
1| Generating public/private rsa key pair.
2| Enter file in which to save the key (/c/Users/you/.ssh/id_rsa):
3| //到这里可以直接回车将密钥按默认文件进行存储
```
然后会出现：
```
1| Enter passphrase (empty for no passphrase):
2| //这里是要你输入密码，其实不需要输什么密码，直接回车就行
3| Enter same passphrase again:
4| 这里再按一次回车
```
接下来屏幕会显示各种字母数字组成的字符串，结尾是你的邮箱，运行以下命令，将公钥的内容复制到系统粘贴板上
```
1| $ clip < ~/.ssh/id_rsa.pub 
```
> 在 GitHub 账户中添加你的公钥

① 登陆 GitHub，进入 Settings：
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/2.png)  
② 点击 SSH and GPG Keys：
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/3.png)  
选择 New SSH key：
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/4.png)
④ 粘贴密钥：
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/5.png)
> 测试

输入以下命令：注意：git@github.com不要做任何更改！
```
1| $ ssh -T git@github.com
```
之后会显示：
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/6.png)
输入 yes 后会显示：
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/7.png)
此时表示设置正确
> 配置 Git 个人信息

Git 会根据用户的名字和邮箱来记录提交，GitHub 也是用这些信息来做权限的处理，输入以下命令进行个人信息的设置，把名称和邮箱替换成你自己的，名字可以不是 GitHub 的昵称，但为了方便记忆，建议与 GitHub 一致
```
1| $ git config --global user.name "此处填你的用户名"
2| $ git config --global user.email "此处填你的邮箱"
```
到此为止 SSH Key 配置成功，本机已成功连接到 Github
> 将本地的 Hexo 文件更新到 Github 的库中

① 登录 Github 打开自己的项目
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/8.png)
② 鼠标移到 Clone or download 按钮，选择 Use SSH
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/9.png)
③ 一键复制地址
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/10.png)
④ 打开你创建的 Hexo 文件夹，右键用记事本（Notepad++或者VS code等都可以）打开该文件夹下的 _config.yml 文件
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/11.png)
⑤ 按下图修改 _config.yml 文件并保存
![alt text](https://raw.githubusercontent.com/chenzhilingq/mytc/master/12.png)
⑥ 在 Hexo 文件夹下分别执行以下命令
```
1| $ hexo g
2| $ hexo d
```
执行完之后会让你输入你的 Github 的账号和密码，如果此时报以下错误，说明你的 deployer 没有安装成功
```
ERROR Deployer not found: git
```
需要执行以下命令再安装一次：
```
1| $ npm install hexo-deployer-git --save
```
再在 Hexo 文件夹下分别执行以下命令
```
1| $ hexo g
2| $ hexo d
```
你的博客就会部署到 Github 上了
⑦ 访问博客
你的博客地址：https://你的用户名.github.io，现在每个人都可以通过此链接访问你的博客了。
