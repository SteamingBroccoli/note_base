# Linux

集合基础知识以及实操经验总结Linux的使用手册

- Linux系统文件结构以及存储方式
- 指令
  - 基础
  - 常用（重点掌握）

- 实操
  - 部署
  - 调试
  - 测试

## 基础知识

=.= 

### Linux系统文件结构













# 分布式版本控制系统

- git

- svn

  

## Git

 Git 是一个分布式版本控制系统，它允许开发者在本地仓库中工作，并可以将更改推送到远程仓库。

### 指令

#### 连接

ssh： git remote add origin git@github.com:SteamingBroccoli/note_base.git

#### 创建以及初始化

```
git init：初始化一个新的 Git 仓库。

git add：将文件添加到暂存区。如果使用 `.` 作为参数，则添加当前目录中的所有文件。
#git add .

git clone：克隆一个远程仓库到本地。
```



#### 查询status 

```
git commit：提交暂存区的更改到本地仓库。可以使用 `-m` 参数来添加提交信息。
#例如：git commit -m “测试”


git reset：重置工作目录或暂存区的文件到某个历史提交。
git branch：查看和操作本地分支。
git checkout：切换到某个分支或查看某个提交的状态。

git push：将本地分支的更改推送到远程仓库。

Git 命令的组合使用可以实现更复杂的操作，例如：
git stash：保存当前工作目录的更改，以便稍后恢复。
git stash apply：应用保存的更改。
git stash drop：删除保存的更改。
git stash clear：删除所有保存的更改。
```



#### 拉取

git merge：将指定的分支合并到当前分支。
git pull：从远程仓库获取并合并分支。







# 数据库



# 服务器

Nginx高性能HTTP/Pr0xy服务器



# 自动化运维



# 运维监控





# 容器虚拟化技术







# 中间件









# 堡垒机

