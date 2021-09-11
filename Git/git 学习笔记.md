## 配置Git

### 设置用户名和邮件地址

```
git config --global user.name "Chen GangQiang"
```

```
git config --global user.email 644076531@qq.com
```

### 查看配置

```
git config --list
```

![image-20210911134142159](.\git.assets\image-20210911134142159.png)

![image-20210911133909522](.\git.assets\image-20210911133909522.png)

## 管理仓库

### 创建本地仓库

```
git init
```

![image-20210911131938832](.\git.assets\image-20210911131938832.png)

### 检测当前文件夹下的文件状态

```
git status
```

![image-20210911131907096](.\git.assets\image-20210911131907096.png)

### 管理文件

```
// 文件名，如果是全部是写.
git add 文件名
```

```
git add .
```

![image-20210911132313045](.\git.assets\image-20210911132313045.png)

*注：被管理的文件变为绿色，没有管理的文件为红色*

### 生成版本

```
git commit -m '第一个版本'
```

![image-20210911134514404](.\git.assets\image-20210911134514404.png)

![image-20210911134547102](.\git.assets\image-20210911134547102.png)

如果对文件进行了修改，再次运行git status，如下:

![image-20210911134813815](.\git.assets\image-20210911134813815.png)

修改文件后，使用git add.后，再次git commit -m '变更记录'

![image-20210911135118811](.\git.assets\image-20210911135118811.png)

### 查看版本记录

```
git log
```

![image-20210911135242280](.\git.assets\image-20210911135242280.png)

```
git log --graph
```

![image-20210911194159903](.\git.assets\image-20210911194159903.png)

```
git log --graph --pretty=format:"%h %s"
```

![image-20210911194357486](.\git.assets\image-20210911194357486.png)

### 文件名的颜色状态

红色：未被管理或修改过的文件，红色变绿色使用git add

绿色：已被git管理，使用git commit -m '' 提交

### 来回切换

提交到暂存区（绿色）

```
git add.
```

返回

```
git reset HEAD
```

![image-20210911152638100](.\git.assets\image-20210911152638100.png)



## 回滚

### git reset

```
git reset --hard 6a67d122e94b8a93537f21e67b63832448ac216d
```

![image-20210911145621119](.\git.assets\image-20210911145621119.png)

回滚之后再回去，需要使用git reflog查看，然后再回滚

![image-20210911150348871](.\git.assets\image-20210911150348871.png)



### git reflog

```
git reflog
```

![image-20210911150213785](.\git.assets\image-20210911150213785.png)



## 分支

### 查看分支

```
git branch
```

![image-20210911154654038](.\git.assets\image-20210911154654038.png)

### 创建分支

```
git branch 分支名
```

![image-20210911154832313](.\git.assets\image-20210911154832313.png)

```
git checkout -b dev
```

![image-20210911223022393](.\git.assets\image-20210911223022393.png)

### 切换分支

```
git checkout dev
```

![image-20210911154952998](.\git.assets\image-20210911154952998.png)

### 合并分支

需要先切换回master分支

![image-20210911155807928](.\git.assets\image-20210911155807928.png)

```
git merge 分支名
```

![image-20210911155944779](.\git.assets\image-20210911155944779.png)

### 删除分支

```
git branch -d 分支名
```

![image-20210911160157463](.\git.assets\image-20210911160157463.png)



## 变基rebase

### 场景1：多个记录合并成一个记录

```
git rebase -i HEAD~3
```

![image-20210911190859689](.\git.assets\image-20210911190859689.png)

把pick改为s，就是合并到上面的版本

![image-20210911191030500](.\git.assets\image-20210911191030500.png)

![image-20210911191224065](.\git.assets\image-20210911191224065.png)

注：合并记录不要合并push的记录

### 场景2：全并分支

第一步：切回子分支

第二步：rebase

第三步：回到主分支

第四步：merge

![image-20210911194754340](.\git.assets\image-20210911194754340.png)

![image-20210911194930841](.\git.assets\image-20210911194930841.png)

![image-20210911195035964](.\git.assets\image-20210911195035964.png)

### 场景3：

公司代码没有提交，家里又写了代码，回公司将两种代码合并，但不产生分支

```
git fetch origun dev
git rebase origun/dev
```

## Beyond Compare使用方法

```
git config --local merge.tool bc

git config --local mergetool.path "C:/Program Files/Beyond Compare/BCompare.exe"

git config --local mergetool.keepBackup false
```

这样配置只对当前项目有效

## Tag

```
git tag -a v1 -m "第一版本"
```

![image-20210911222621239](.\git.assets\image-20210911222621239.png)

提交到github

```
git push orighin --tags
```

## 配置信息 git config

### 项目配置文件

```
git config --local --list
```

目录在：.git/config

### 全局配置文件

```
git config --global --list
```

系统当前用户所在目录：~/.gitconfig

### 系统配置文件

```
git config --system --list
```

```
查看仓库级的 config，命令：git config –local -l
查看全局级的 config，命令：git config –global -l
查看系统级的 config，命令：git config –system -l
查看当前生效的配置，  命令：git config -l
```



## git remote add origin

```
git remote add origin 链接地址
```

默认添加到了local



## 免密登录

### 1.URL方式

```
原来的地址：https://github.com/qq644076531/KeePassDatabase.git
修改的地址：https://用户名:密码@github.com/qq644076531/KeePassDatabase.git

git remote add origin https://用户名:密码@github.com/qq644076531/KeePassDatabase.git
git push origin master
```

### 2.ssh实现

```
1.生成公钥和私钥（默认放在~/.ssh目录下，id_rsa.pub公钥	id_rsa私钥）
ssh-keygen
2.拷贝公钥内容，并设置到github中
3.在git本地中配置ssh地址
git remote add origin git@github.com:qq644076531/KeePassDatabase.git
```



![image-20210911233020343](.\git.assets\image-20210911233020343.png)

![image-20210911233434203](.\git.assets\image-20210911233434203.png)



## git忽略文件

```
vim .gitignore
```





