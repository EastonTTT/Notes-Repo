 ## 合并到上一次提交：
总会遇到，已经提交了代码但是又发现有一些小地方有改动，这个时候可以通过以下命令，将细小的改动合并到上次的提交中，而不是新增一次提交，污染提交记录。
1. `git add .`
2. `git commit --amend --no-edit` 把新的改动合并进上一次提交中，而不产生一个新的提交。如果这里去掉`no-edit` 则可以修改提交message
3. `git push -force-with-lease` 带有安全锁的覆盖远程分支。远程分支的最新提交 **必须** 跟你本地拉取时看到的远程分支是**同一个提交**，才会覆盖，否则会拒绝推送。
---
## 连接问题：

```bash
$ git pull
ssh: connect to host github.com port 22: Connection refused
fatal: Could not read from remote repository.
​
Please make sure you have the correct access rights
and the repository exists.
```
ssh是通过22端口连接GitHub的，由于种种原因这个端口被拦截了，所以要在ssh配置文件里面切换访问GitHub的端口，将端口切换为443一般即可解决问题。
### 测试连接是否正常：
使用命令：`ssh -T git@github.com`测试能否连接上。
使用命令：`ssh -vvT git@github.com`用来输出具体日志，排查具体问题原因。
### 切换方法：
找到`~/.ssh/config`文件，如果没有就新建一个。把一下文字粘贴到里面：
```bash
Host github.com
HostName ssh.github.com
User git
Port 443
IdentityFile ~/.ssh/id_rsa   # 如果你用 id_rsa，就改成 ~/.ssh/id_rsa
IdentitiesOnly yes
```
---
## 创建线上同名分支：

```git
git checkout -b mybranch origin/mybranch
```
