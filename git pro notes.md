---
title: git pro notes
date: 2020-05-15 17:23:44
tags:
	-git
keywords:
cover: https://cdn.jsdelivr.net/gh/Eastwood6/Eastwood6.github.io@master/img/https.jpg
abbrlink:
top_img: https://cdn.jsdelivr.net/gh/Eastwood6/Eastwood6.github.io@master/img/TB10Vh7SpXXXXbZaFXXXXXXXXXX-2880-1080.jpg
---

pro git 2nd edition
%HOMEDRIVE%%HOMEPATH%
[TOC]
## Getting Started

## Git Basics
**git较其他vcs特点**

- nearly every operation is local
- integrity
- only add
- three states: unmodified,modified,staged
(当你对modified文件staged,这些文件保存在staging area,然后会snapshot，当你commit的时候，文件还是在staging area，snapshots永久保存至git repository)

---
- Getting a Git Repository
create local Repository
`git init` create a skeleton,if you wanna track these files:
```
  $ git add *.c
  $ git add LICENSE
  $ git commit -m 'initial project version'
```
copy from remote server
```
git clone url (name)
```
**以上文件系统自动帮你commit**
-  Recording Changes to the Repository
1. Staging Modified Files:
当git add后再修改该文件，git status查看时，会发现
Changes to be committed，Changes not staged for commit:
都有该文件，git add track 的是当时的版本，修改后并没有重新track

2. Short Status:
`git status -s or git status --short`
左边的表示staged,右边的表示modified，
修改一个文件时，是右边的M，add后是左边的M,在修改如果是本地文件是MM，如果是新建文件是AM，未作修改??

3. Ignoring Files
语法:  P46 
>gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。

4. Viewing Your Staged and Unstaged Changes
`git diff`
git diff 比较的是staging area与原文件的不同
`git diff --staged` 比较的是当前staged与last commit区别，如果没有commit，就是原文件
`git diff --cached` 展示staged area

5. Committing Your Changes
commit之前可以先git status看下是否都在staged area,git commit也会将编辑器选项带过去
git commit 你会看到最新git status output,去掉注释或加一段message以留下commit message 
`git commit -m “message”`直接留下message提交
`git commit -v `可以看到即将要提交哪些更改

6. Skipping the Staging Area
>command makes Git automatically stage every file that is already **tracked** before doing the commit, letting you skip the git add part

跳过git add直接将修改未staged git commit
`git commit -a/git commit -a -m 'message'/git commit -am 'message'
`
7. Removing Files
`rm `删除working directory文件
`git rm `同时删除index(staging area)和working directory文件
(**commit 过的文件git rm没有提示，没有commit过的staged file会提示：**`the following file has changes staged in the index(use --cached to keep the file, or -f to force removal)`)(因为没有提交而无法恢复所以怕你误删)
`git rm --cached README` git不再tracking README,改为本地保存
` git rm log/\*.log` 删除指定目录
` git rm \*~ `删除所有以`*`结尾的文件

 8. Moving Files
` rm/git rm oldname newname;`

- Viewing the Commit History
` git log` 查看项目提交完整记录 
 显示格式 P58   显示命令P60     显示输出限制P60
 `git log -p/-p -num` 查看项目提交完整详细记录/查看**最近**指定数目
 `git log --stat `查看类似 1 file changed, 0 insertions(+), 0 deletions(-)
 `git log --pretty=oneline` 简略输出一行 )
 `git log --pretty=format:"%h %s" --graph`(显示我的分支与合并历史)
 `git log --grep` 搜索commit message里的关键词
 `git log -S `搜索新增或删除代码里的关键词

- Undoing Things
1. `git commit (-m msg)--amend` 再次提交staging area(以防提交后忘了提交某文件或者想修改commit message)
2. Unstaging a Staged File 
`git reset [FILE]`
3. Unmodifying a Modified File
`git checkout [FILE] `(撤销就无法反撤销了，记住commit过的文件都有备份，但没有commit的没有备份)

- Working with Remotes
1. Showing Your Remotes
`git remote`查看你有配置过哪些remote servers,展示了每个你所明确的简称
`git remote -v` 查看简称与url
2. Adding Remote Repositories
`git remote add [shortname]  [url]`
3. Fetching and Pulling from Your Remotes
`git fetch [shortname]`  远程下载文件到相应分支中,(switch branch and will update automatically)

`git pull shortName branchName` ,远程下载文件到相应分支中，automatically tries to merge it into the code you’re currently working on.

4. Pushing to Your Remotes
`git push shortName branchName( :replaceName ) ` 
- (This command works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime)
-  push前所做的修改要提交
-  (新的branchName会自动创建branch)
 `git config --global credential.helper cache`(DONT TYPE YOUR PASSWORD EVERY TIME)
5. Inspecting a Remote
`git remote show [shortName]`(在线查看shortName的branches、 head branch、pull、push url)
6. Removing and Renaming Remotes
`git remote rename pb paul`
`git remote rm paul`
- Tagging
>Typically people use this functionality to mark release points
1. Listing Your Tags
`git tag`  Listing the available tags
`git tag -l (name)`   search tag
2. Creating Tags
3. Annotated Tags
`git tag -a tagname (-m tagMsg)`
`git tag show` tagname  (show  the tag data along with the commit)
4. Lightweight Tags 
`git tag tagname`  (and `git tag show` dont show any information except commit)
5. Tagging Later
`git tag -a tagname commiit checksum (or part of it)`
6. Sharing Tags 
`git push origin [tagname]`
`git push origin --tags` (transfer all of your tags to the remote server that are not already there)
7. Checking out Tags
`git checkout -b version2 v2.0.0` (create a new branch at a specific tag)
- Git Aliases
`git config --global alias.custWords comands`
eg: 
```
git config --global alias.co checkout,
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
```

## Git Branching
查看Git repository 保存哪些东西 P78 
(git use the HEAD pointer to which the local branch you're currently on,when you commit ,it will point to the latest commit automatically,when you use git checkout command,the HEAD switched to the branch you point to)

- Branches in a Nutshell 

1. Creating a New Branch
`git branch branchName `(create a new branch )
2. Switching Branches 
>note that if your working directory or staging area has uncommitted changes that conflict with the branch you’re checking out, Git won’t let you switch branches

`git checkout branchName`

`git log --oneline --decorate` (show which branch you currently are)

`git log --oneline --decorate --graph --all` (show branch relation map)
- Basic Branching and Merging 
1. Basic Branching
`git checkout -b branchName` (create and enter that branch)
`git branch -d branchName` delete a branch
2. Basic Merging 
`git merge branchName `
**fast forward**    
>To phrase that another way, when you try to merge one commit with a commit that can be reached by following the first commit’s history, Git simplifies things by moving the pointer forward because there is no divergent work to merge together
>**'recursive' strategy** p92
3. Basic Merge Conflicts 
If you changed the same part of the same file differently in the two branches you’re merging together, Git won’be able to merge them cleanly
you get the warning after command git merge,you update the files,remove the conflict  in the file ,git add,and commit.  

`git mergetool `(list useful tools)

**every updated file is synchronized in each  branch after merging**
- Branch Management 
`git branch`  (list branch)
`git branch -v`(To see the last commit on each branch)
`git branch --merged`
`git branch --no-merged`

- Branching Workflows 
1. Long-Running Branches 
stable branch->master
parallel branch->develop/next（used to test stability,whenever it gets to a stable state, it can be merged into master.It’s used to pull in topic branches (short-lived branches, like your earlier iss53 branch) when they’re ready, to make sure they pass all the tests and don’t introduce bugs.）

2. Topic Branches 
这种工作流其实就是创建多种分支，不同的分支不同的目的，可以merge也可以delete,最终是为了这个Topic，所以叫Topic Branches Workflows
- Remote Branches 
1. Pushing 
2. Tracking Branches 
`git checkout -b sf origin/serverfix`  create and use cusName to track remote branch branchName>ones that track branches on other remotes, or don’t track the master branch.

`git branch -u origin/serverfix`

`git branch -vv`  list out your local branches with more information including what each branch is tracking and if your local branch is ahead, behind or both.
3. Pulling
4. Deleting Remote Branches 
 `git push origin --delete serverfix` delete your serverfix branch from the server,not local
- Rebasing 
1. The Basic Rebase 
`git rebase master`
rebase and merge 最终的snapshot相同只是历史不同，rebase按直线提交，而merge按终点提交

2. More Interesting Rebases 
`git rebase [basebranch] [topicbranch]` 
3. The Perils of Rebasing 
4. Rebase When You Rebase 
5. Rebase vs. Merge 
## Git on the Server

- The Protocols 122

1. Local Protocol 122

2. The HTTP Protocols 123

3. The SSH Protocol 126

4. The Git Protocol 126

- Getting Git on a Server 127
`git clone --bare my_project my_project.git` clone your repository to create a new bare repository
`cp -Rf my_project/.git my_project.git`
1. Putting the Bare Repository on a Server 128

`scp -r my_project.git user@git.example.com:/opt/git` store all your
Git repositories under the /opt/git directory.
`git clone user@git.example.com:/opt/git/my_project.git`other users who have SSH access to the same server which has read-access to the /opt/git directory can clone your repository by running

```
$ ssh user@git.example.com
$ cd /opt/git/my_project.git
$ git init --bare --shared
```
>a user SSHs into a server and has write access to the /opt/git/my_project.git directory, they will also automatically have push access.
>Git will automatically add group write permissions to a repository properly if you run the git init command with the --shared option.
2. Small Setups 129
- Generating Your SSH Public Key 130
>By default, a user’s SSH keys are stored in that user’s ~/.ssh directory

`ssh-keygen`  If you don’t have a pair of files named something like id_dsa or id_rsa (or you don’t even have a .ssh directory)

[creating an SSH key](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)
- Setting Up the Server 131
```
$ sudo adduser git
$ su git
$ cd
$ mkdir .ssh && chmod 700 .ssh
$ touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
```
create a git user and a .ssh directory for that user.

- Git Daemon 134

- Smart HTTP 135

- GitWeb 137

- GitLab 140

1. Installation 140

2. Administration 141

3. Basic Usage 144

4. Working Together 144

- Third Party Hosted Options 145

## Distributed Git
- Distributed Workflows 147

1. Centralized Workflow 147

2. Integration-Manager Workflow 148

3. Dictator and Lieutenants Workflow 149

4. Workflows Summary 150

- Contributing to a Project 151

1.  Commit Guidelines 151
 `git diff --check`

 try to make each commit a logically separate changeset 

- use the staging area on Monday to split your work into at least one commit per issue, with a useful message per commit. If some of the changes modify the same file, try to use git add -- patch to partially stage files (covered in detail in “Interactive Staging”).
- The project snapshot at the tip of the branch is identical whether you do one commit or five 
- This approach also makes it easier to pull out or revert one of the changesets if you need to later. “Rewriting History” describes a number of useful Git tricks for rewriting history and interactively staging files 
- your messages should start with a single line that’s no more than about 50 characters and that describes the changeset concisely, followed by a blank line, followed by a more detailed explanation
2. Private Small Team 153

3. Private Managed Team 160
**开发者无法合并到主分支，需要邮件或联系integrator who merge the branches that already pushed to the server**

`git push -u origin brannch`  设置默认remote server
`git push origin  master:branch` master覆盖remote shit branch

4. Forked Public Project 166
**开发者无法更新 branch on the project,需要fork project,然后push to the server, pull request**
`git push -f myfork featureA`
`git request-pull origin/master myfork`
5. Public Project over E-Mail 170

`git format-patch -M origin/master`    it turns each commit into an e-mail message with the first line of the commit message as the subject and the rest of the message plus the patch that the commit introduces as the body.

`git send-email *.patch`  the file you send must have format-patch as above and setting up in file .config
6. Summary 173

- Maintaining a Project 173
1.  Working in Topic Branches 174
` git branch sc/ruby_client master` create the branch based off your master branch like this
2. Applying Patches from E-mail 174

3. Checking Out Remote Branches 178

4. Determining What Is Introduced 179

5. Integrating Contributed Work 180

6. Tagging Your Releases 187

7. Generating a Build Number 188

8. Preparing a Release 189

9. The Shortlog 189


## GitHub
notes:
**pull request之后，该请求分支里的修改会自动更新到pull request中**
**collaborator是无法merge branch的,所以也有pull request，所以pull request指的都是请求merge branch**
- Account Setup and Configuration 191

1. SSH Access 192

2. Your Avatar 194

3. Your Email Addresses 195

4. Two Factor Authentication 196

- Contributing to a Project 197
 1. Forking Projects 197

 2. The GitHub Flow 198
 `git diff master shit` 比较branch区别

 pull request：
 当repository有pull request时，对repository有写权限的人才会看到
 merge pull request button,当你merge时，不会是fast-forward方式，github只会创建merge commit,除非clone到本地操作再push到github,pull request会自动消失

 3. Advanced Pull Requests 206
REFERENCES:
可以利用 #  来引用pull request,commit(SHA),issue
 4. Markdown 211
    有上面标识默认是markdown格式

![968743b0d1f92f77fa07a7779b2d5cc5.png](pic/Image [2].png)

###### Task Lists:
   在pull request description里写task list 会在 pull request里看到

![e8b6842a63e823c12eea086ca3cef036.png](pic/Image [3].png)

###### Quoting:
  用'>'符号引用一段别人的评论/直接框选一段评论按R key，回复comment
###### Emoji:
start with a ` : ` character, an autocompleter will help you find what you’re looking for
###### Images: 
you can drag or drop
- Maintaining a Project 216
1. Creating a New Repository 216

2. Adding Collaborators 218

3. Managing Pull Requests 220
*将指定pull request保存至本地*：
`git ls-remote url` get a list of all the branches and tags and other references in the repository

SHA   refs/heads/sda        --> branches
SHA   refs/pull/1/head      --> sha(last commits sha to this (#num)                                           pull request )
SHA   refs/pull/3/merge    --> represents the commit that would                             result if you push the “merge”button on the site.
`git fetch origin refs/pull/958/head`pull down every Pull Request branch in one go without having to add a bunch of remotes.
*将所有pull request refs保存至本地*：
```
[remote "origin"]
url = https://github.com/libgit2/libgit2.git 
fetch = +refs/heads/*:refs/remotes/origin/*
fetch = +refs/pull/*/head:refs/remotes/origin/pr/*
```
编辑.git/config 然后`git fetch` 到本地refs/remotes/origin/pr/,想切换到哪个分支就` git checkout pr/num` ，
4. Mentions and Notifications 225
@ character and it will begin to autocomplete with the names and usernames of people who are collaborators or contributors in the project.You can also mention a user who is not in that dropdown
 5. Special Files 229README 229

 6. CONTRIBUTING 230

 7. Project Administration 230

- Managing an organization 232
1. Organization Basics 232

2. Teams 233

3. Audit Log 235

- Scripting GitHub 236
1. Hooks 237

2. The GitHub API 241

3. Basic Usage 242

 4. Commenting on an Issue 243

 5. Changing the Status of a Pull Request 244

 6. Octokit 246


## Git Tools
## Customizing Git
## Git and Other Systems
## Git Internals

[TOC]

issues

   2. 测试： fast forward 合并两个文件同步吗  一个branch amend或commit /master 还在 git branch --merged吗recursive' strategy呢

note:
1. 新创建的要add,本地的原来的不用add
2. git commit -a -m ''/git commit --amend  区别在于 
amend只是修改当前提交，做过的修改还要add,
而 -a 跳过add命令并创建了一个新提交
3. 一个分支创建另一个分支 会显示在该分支的git branch --merged里

ssh:
1. xshell登录server时 ，用xshell自带的生成公钥并保存至server authorized_keys中，xshell会自动用私钥登录


config:
git config commands作用在C:\Users\hp\.gitconfig里

email:
    .gitconfig可以设置收发人
    好像只能发明文
    Gmail[详见](https://www.juvenal.me/personal/learning/2017/07/26/using-git-send-email-with-gmail-tls-on-macos/)https://www.juvenal.me/personal/learning/2017/07/26/using-git-send-email-with-gmail-tls-on-macos/)
