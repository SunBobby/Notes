# Git常用命令
> git操作汇总及备忘录
## 基础设置
- 初始化git仓库
```bash
git init
```
- 设置git账户
```bash
git config --global user.name "zcy"
git config --global user.email a@b.com
```
- 配置信息相关操作
```bash
git config --list #查看当前所有config信息
```
- 状态记录
```bash
git add . # 将当前文件夹内所有修改加入到暂存区
git status # 查看暂存区当前跟踪状态（加上-s可以查看精简输出）
```
- 比较
```bash
git diff # 比较当前工作区暂存快照和未暂存文件之间的差异
git diff --staged # 比较暂存区快照和最后一次提交之间的差异
```
- 提交文件
```bash
git commit -m "xxx" # 提交并且添加提交说明
```
- 移动、删除
```bash
git mv xx cc # 移动文件
git rm xx # 删除文件
```
### 贮藏与清理
```bash
git stash # 将暂存未提交的数据通过一个栈保存下来
git stash push # 同上
git stash list # 查看所有贮藏
git stash drop stash_name # 删除贮藏
git stash clear # 删除所有缓存stash
```
- 贮藏重新应用
```bash
git stash pop # 删除缓存对战第一个stash并且应用到当前目录
git stash apply # 与pop相比补删除stash拷贝
```
- 查看特定stash的diff
```bash
git stash show
git stash show -p # 查看特定stash全部diff
```
- 从stash新建分支
```bash
git stash branch new
```
- 清理工作目录
```bash
git clean # 清理工作目录
```
## 远程仓库
- 初始化本地密钥
```bash
ssh-keygen -t rsa -C "远程地址"
```
- 查看远程仓库
```bash
git remote -v # 显示远程仓库
git remote show origin # 显示远程仓库
git remote rename # 远程仓库重命名
git remote add origin git@xxx.com # 添加远程地址
git remote rm origin # 删除origin远程
```
- 推送
```bash
git push origin main
```
- 拉取
```bash
git pull origin main
```
- 远程仓库
```bash
git clone https://xx/xx # 克隆现有仓库
```
- **提交历史**
```bash
git log # 查看提交历史
git log -p # 显示每次提交所引入的差异
git log --stat # 查看每次提交统计信息
git log --pretty=full/short/fuller # 使用不同方式展现提交历史
```
- 撤销操作
```bash
git commit --amend # 用于修改并替换上一次提交内容
git chechout -- file.name # 撤销对文件的修改
```
- 取消暂存
```bash
git reset # 撤销
```
## 分支管理
- 创建分支与切换分支
```bash
git branch dev # 创建dev分支
git checkout dev # 切换到dev分支
git checkout -b dev # 上述两条之和
```
- 合并分支
```bash
git checkout main # 首先切换到主分支
git merge dev # 合并开发分支上的修改
git status # 查看冲突
```
- 删除分支
```bash
git branch -d dev # 删除dev分支
```
### 变基
```bash
git checkout dev # 切换到dev分支
git rebase main # 提取dev中的修改然后应用到main分支上来
# 
git rebase main dev # 将dev变基到main上
# 快进主分支
git checkout main
git merge dev
```
- 分支状态
```bash
git branch # 标识所有分支
git branch -v # 查看每个分支最后一次提交
git branch --merged # 查看已经合并到当前分支的分支
git branch --no-merged # 未合并到当前分支的
```
- 解决冲突
```bash
git add . # 添加修改后的文件
git rebase --continue # 继续rebase
```
## 标签管理
```bash
git tag # 显示标签
git tag -l "v1.1" # 查找特定标签
```
- 附注标签
```bash
git tag -s v2 -m "instruction" # -a指定标签。
git show v2 # 显示与标签对应的信息
```
>存储完整对象
- 轻量标签
```bash
git tag v2 # 打标签
```
- 补充标签
```bash
git tag -a v2.1 校验和 # 校验和是log上的部分校验和或者完整校验和
```
- 推送标签
```bash
git push origin v2.1 # 推送到origin
git push origin --tags # 推送所有标签
```
- 删除标签
```bash
git tag -d v2.1 # 删除v2.1标签
```
- 检出标签
```bash
git checkout v2 # 切换到标签分支，但是处于分离头指针状态，修改无法被追踪
git checkout -b v2 # 切换到新建分支
```
# 搭建Git服务器
>...