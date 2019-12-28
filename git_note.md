##廖雪峰 git 教学
|命令|解释|目录|
|------|-----|------|
|git config --global user.name `""`|设置用户名 `""`|创建版本库|
|git config --global user.email `""`|设置用户email `""`|创建版本库|
|mkdir `""`|创建文件夹 `""`|创建版本库|
|cd `""`  <br>  cd `..`|移动至 `""`  <br>  移动至上层文件夹|创建版本库|
|pwd `""`|当前位置|创建版本库|
|git init|把这个目录变成Git可以管理的仓库|创建版本库|
|git add `"filename"`|告诉Git，把文件`"filename"`添加到仓库（步骤1）|版本退回|
|git commit -`"message"`|告诉Git，把文件`"a"`提交到仓库，并且添加注释为`"message"`（步骤2，可以add多个文件，然后一次commit）|版本退回|
|git diff `"filename"`|`git init` 之后，在文件夹下添加和修改文件，在`add`之前，可以比较修改文件前后变化（实际上是工作区和版本库间的比较）|版本退回|
|git status|仓库当前的状态|版本退回|
|git log<br>git log --pretty=oneline  <br>  git reflog|查看对仓库操作历史;  <br>  简化显示;  <br>  查看对仓库操作的以往历史|版本退回|
|git reset HEAD^  <br>  git reset HEAD^^  <br>  git reset HEAD~`"n"`  <br>  git reset --hard  <br>  git reset --mixed|倒退回前一版本;  <br>  两个版本前的版本;  <br>  n个版本之前的版本，默认参数为--mixed，表示commit退回先前版本，但差异部分存储在工作区  <br>  参数--hard表示commit退回先前版本，并且将版本间差异删除，不存放在工作区|版本退回|
|git reset --hard `"commidid"`|倒退到commitid为`"commitid"`的版本（commitid可以只写部分）|版本退回|
|![工作区和版本库](https://static.liaoxuefeng.com/files/attachments/919020037470528/0)||工作区和版本库|
|![git add 的本质](https://static.liaoxuefeng.com/files/attachments/919020074026336/0)|git add命令实际上就是把要提交的所有修改放到暂存区（Stage）|工作区和版本库|
|![git comit 的本质](https://static.liaoxuefeng.com/files/attachments/919020100829536/0)|执行git commit就可以一次性把暂存区的所有修改提交到分支|工作区和版本库|
|git diff HEAD -- `"filename"`|命令可以查看工作区文件`"filename"`和版本库里面最新版本的区别|管理修改|
|git restore `"filename"`|意思就是，把filename文件在工作区的修改全部撤销（清空工作区）|撤销修改|
|git  restore --staged `"filename"`|可以把暂存区的修改撤销掉（unstage），重新放回工作区（清空版本库的stage）|撤销修改|
||如果已经git add 并且git commit，则只能通过版本退回方式把HEAD指向以前版本|撤销修改|
|git rm `"filename"`|在版本库的stage里删除文件|删除文件|
|git checkout --`"filename"`|用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”|删除文件|
|git push `origin` `branch`|只要本地作了提交，就可以通过命令把本地分支`branch`的最新修改推送至GitHub,默认远程仓库名称为origin|添加远程库|
|git remote -v|查看远程库的信息|添加远程库|
|git clone `path`|从远程仓库克隆文件夹，默认情况下，只能克隆远程仓库的master分支，如果需要克隆其他分支，需要git checkout -b `dev origin/dev`|克隆远程仓库|
|git checkout -b `"branch"`  <br> =  <br> git branch `"branch"` <br> + <br> git checkout `"branch"` <br> =  <br>  git switch -c `'branch'` <br> = <br> git branch `'branch'` <br> + <br> git switch `'branch'`|创建`"branch"`分支，然后切换到`"branch"`分支| - 分支管理  <br> - 创建与合并分支|
|git branch|命令查看当前分支| - 分支管理  <br> - 创建与合并分支|
|git merge -m `'comment'` `'branchname'`  <br>  git merge --no--ff|用于合并指定分支`'branchname'`到当前分支，并添加注释`'comment'`  <br>  `'--no--ff'` 命令可以使得在`'git log`时可以显示分支合并图| - 分支管理  <br> - 创建与合并分支|
|git branch -d `'branchname'`|删除分支| - 分支管理  <br> - 创建与合并分支|
||因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。||
|git log --graph|命令可以看到分支合并图| - 分支管理  <br> - 解决冲突|
|![分支管理策略](https://static.liaoxuefeng.com/files/attachments/919023260793600/0)|多人合作开发时，master分支用于存放稳定版本，开发工作在dev上进行。当多人合作时，每人均有自己的分支，并由dev合并多人工作，当需要发布稳定版本时，由master分支合并dev分支| - 分支管理  <br> - 分支管理策略|
|git stash|工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作|bug分支|
|git stash list|刚才的工作现场存到哪去了？用git stash list命令看看|bug 分支|
|git stash apply  <br>  git stash drop  <br>  git stash pop|用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除;  <br> 另一种方式是用git stash pop，恢复的同时把stash内容也删了|bug 分支|
|git cherry-pick `commitid`|在master分支上修复了bug后，我们要想一想，dev分支是早期从master分支分出来的，所以，这个bug其实在当前dev分支上也存在。Git专门提供了一个cherry-pick命令，让我们能复制一个特定的提交到当前分支|bug 分支|
|git stash `stashid`|可以指定恢复至`git stash list`中的哪个状态|bug分支|
||开发一个新feature，最好新建一个分支；如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。|feature分支|
|git pull  <br> <br> git branch --set-upstream-to <branch-name> origin/<branch-name> |多人协作的工作模式通常是这样：<br>首先，可以试图用git push origin <branch-name>推送自己的修改；<br>如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；<br>如果合并有冲突，则解决冲突，并在本地提交；<br>没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！<br>如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。|多人协作|
|
