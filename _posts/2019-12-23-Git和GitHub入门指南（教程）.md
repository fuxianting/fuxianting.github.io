# Git和GitHub入门指南（教程）

## 简介

![0ee48652-14c2-4be1-ae50-b7d56578e6be](C:\Users\Administrator\Desktop\2019-CQUE-translation-project-management-final-\附件2 translation project\An Intro to Git and GitHub for Beginners (Tutorial)_files\0ee48652-14c2-4be1-ae50-b7d56578e6be.webp)

8月，我们在HubSpot主持了<font color="#6495ED">**“女性编码”**</font>会议，并针对初学者主持了有关使用git和GitHub的研讨会。 我首先浏览了有关git的基础知识和背景的幻灯片演示，然后我们分成小组来运行我创建的用来模拟大型协作项目的教程。 活动结束后我们得到了反馈，它是一个实用的<font color="#6495ED">**动手介绍** </font>因此，如果您还是git的新手，请按照以下步骤操作，以轻松地更改代码库，打开拉取请求（PR）并将代码合并到master分支中。 任何重要的git和GitHub术语均以粗体显示，并带有指向官方git参考资料的链接。

# 准备工作：安装git并创建一个GitHub帐户

你需要做的前两件事是安装git并创建一个免费的GitHub帐户。

请按照<font color="#6495ED">**此处**</font>的说明安装git（如果尚未安装）。 请注意，对于本教程，我们将仅在命令行上使用git。 尽管有一些很棒的git GUI（图形用户界面），但我认为先使用git特定的命令学习git，然后在熟悉该命令后尝试git GUI会更容易。

完成此操作后，在<font color="#6495ED">**此处**</font>创建一个GitHub帐户。 （公共仓库是免费的，但私人仓库是收费的。）

# 步骤一：建立本地git存放区

使用git在本地计算机上创建新项目时，首先要创建一个新的<font color="#6495ED">**仓库**</font>（或简称为“ **repo**”）。

要使用git，我们将使用终端。 如果您对终端和基本命令没有太多了解，请查看<font color="#6495ED">**本教程**</font>（特别是“导航文件系统”和“移动”部分）。

首先，打开一个终端，然后使用cd（更改目录）命令移动到要在本地计算机上放置项目的位置。 例如，如果您的桌面上有一个“项目”文件夹，则可以执行以下操作：

```html
mnelson:Desktop mnelson$ cd ~/Desktop
mnelson:Desktop mnelson$ mkdir myproject
mnelson:Desktop mnelson$ cd myproject/
```

 [gitinit.md](https://gist.github.com/cubeton/89793ba1bc947f64658e#file-gitinit-md) hosted with ❤ by [GitHub](https://github.com)

```html
mnelson:Desktop mnelson$ cd ~/Desktop
mnelson:Desktop mnelson$ mkdir myproject
mnelson:Desktop mnelson$ cd myproject/
```

[view raw](https://gist.github.com/cubeton/67a84eb876984f0b5785/raw/d4560016d742865c1fd68d97fcff1feb557d5e19/terminalcd.md)[terminalcd.md](https://gist.github.com/cubeton/67a84eb876984f0b5785#file-terminalcd-md) hosted with ❤ by [GitHub](https://github.com/)

要在文件夹的根目录中初始化git仓库，请运行<font color="#6495ED">**git init**</font>命令：

```
mnelson:myproject mnelson$ git init
Initialized empty Git repository in /Users/mnelson/Desktop/myproject/.git/
```

[view raw](https://gist.github.com/cubeton/89793ba1bc947f64658e/raw/f3dba1dd72fda5eeb98b761338aedfc310d29d54/gitinit.md)[gitinit.md](https://gist.github.com/cubeton/89793ba1bc947f64658e#file-gitinit-md) hosted with ❤ by [GitHub](https://github.com)

```
mnelson:myproject mnelson$ git init
Initialized empty Git repository in /Users/mnelson/Desktop/myproject/.git/
```

[view raw](https://gist.github.com/cubeton/89793ba1bc947f64658e/raw/f3dba1dd72fda5eeb98b761338aedfc310d29d54/gitinit.md)[gitinit.md](https://gist.github.com/cubeton/89793ba1bc947f64658e#file-gitinit-md) hosted with ❤ by [GitHub](https://github.com/)

# 步骤二：添加一个新文件到仓库

接下来，使用你喜欢的任何文本编辑器或运行<font color="#6495ED">**touch**</font>命令将新文件添加到项目中。

在包含git仓库的文件夹中添加或修改文件后，git会注意到该仓库内部已进行了更改。 但是，除非你明确告知git，否则git不会正式跟踪该文件（即，执行提交命令，接下来我们将详细讨论提交）。

```htlm
mnelson:myproject mnelson$ touch mnelson.txt
mnelson:myproject mnelson$ ls
mnelson.txt
```

 [gitstatus.md](https://gist.github.com/cubeton/02e849bbffcbea1e9a61#file-gitstatus-md) hosted with ❤ by [GitHub](https://github.com) 

```htlm
mnelson:myproject mnelson$ touch mnelson.txt
mnelson:myproject mnelson$ ls
mnelson.txt
```

 [gitstatus.md](https://gist.github.com/cubeton/02e849bbffcbea1e9a61#file-gitstatus-md) hosted with ❤ by [GitHub](https://github.com) 

创建新文件后，可以使用<font color="#6495ED">**git status**</font>命令查看git知道存在的文件。

```htlm
mnelson:myproject mnelson$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	mnelson.txt

nothing added to commit but untracked files present (use "git add" to track)
```

 [gitstatus.md](https://gist.github.com/cubeton/02e849bbffcbea1e9a61#file-gitstatus-md) hosted with ❤ by [GitHub](https://github.com/) 

这基本上是说，“嘿，我们注意到你创建了一个名为 mnelson.txt 的文件。但除非你执行'git添加'命令，否则我们将不会对其进行任何处理。”



#### 一个小插曲:暂存环境、提交和操作者

初学git时最容易混淆的部分之一是暂存环境的概念及其与提交的关系。

<font color="#6495ED">**提交**</font>是自上次提交以来你更改了哪些文件的记录。 本质上，您可以对仓库进行更改（例如，添加文件或修改文件），然后告诉git对这些文件执行提交命令中。

提交构成了项目的本质，并允许您随时回到项目状态。

那么，如何告诉git提交哪些文件呢？ 这就是<font color="#6495ED">**暂存环境**</font>或<font color="#6495ED">**索引**</font>的引入。如步骤2所示，当您对仓库进行更改时，git会注意到文件已更改，但不会对其进行任何操作（例如在提交中添加文件）。

要将文件添加到提交中，首先需要将其添加到暂存环境中。 为此，您可以使用<font color="#6495ED">**git add** </font><filename>命令（请参见下面的步骤3）。

使用git add命令将所需的所有文件添加到暂存环境后，您可以使用<font color="#6495ED">**git commit** </font>命令告诉git将它们打包到提交中。

注意：暂存环境，也称为“暂存”，是新的首选术语，但你也可以将其称为“索引”。

# 步骤三:将文件添加到暂存环境

使用git add命令将文件添加到暂存环境。

如果重新运行git status命令，则会看到git已将文件添加到暂存环境（请注意“要提交的更改”行）。

```htlm
mnelson:myproject mnelson$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   mnelson.txt
```

[addtostaging.md](https://gist.github.com/cubeton/28f7bea3b232f67e031c#file-addtostaging-md) hosted with ❤ by [GitHub](https://github.com)

```htlm
mnelson:myproject mnelson$ git status
On branch master

Initial commit

Changes to be :
  (use "git rm --cached <file>..." to unstage)

	new file:   mnelson.txt
```

[addtostaging.md](https://gist.github.com/cubeton/28f7bea3b232f67e031c#file-addtostaging-md) hosted with ❤ by [GitHub](https://github.com/)

重申一下，该文件尚**未**添加到提交中，但即将添加到提交中。

# 步骤四：创建提交

现在可以创建你的第一次提交了！

运行命令git commit -m“您有关提交的消息”

```
mnelson:myproject mnelson$ git commit -m "This is my first commit!"
[master (root-commit) b345d9a] This is my first commit!
 1 file changed, 1 insertion(+)
 create mode 100644 mnelson.txt
```

[commit.md](https://gist.github.com/cubeton/1068d965d147b4039e4d#file-commit-md) hosted with ❤ by [GitHub](https://github.com)

```
mnelson:myproject mnelson$ git commit -m "This is my first commit!"
[master (root-commit) b345d9a] This is my first commit!
 1 file changed, 1 insertion(+)
 create mode 100644 mnelson.txt
```

[commit.md](https://gist.github.com/cubeton/1068d965d147b4039e4d#file-commit-md) hosted with ❤ by [GitHub](https://github.com/)

提交末次修改应该与提交所包含的内容有关，它可能是新添内容，可能是对某一错误思维修改，也可能只是在修复输入错误。 不要输入“ asdfadsf”或“ foobar”之类的内容。这让看到你的提交内容的人很迷茫。

# 步骤五：创建一个新分支

现在，你已经进行了新的提交，让我们尝试一些更高级的东西。

假设你要制作新内容，但担心在制作时会对主项目进行更改。这时候纪要涉及到<font color="#6495ED">**git分支**</font>的内容。

分支允许你在项目的“状态”之间来回切换。 例如，如果要向网站添加新页面，则可以仅为该页面创建一个新分支，而不会影响项目的主要部分。 完成页面后，你可以将分支中的更改<font color="#6495ED">**合并**</font>到master分支中。 创建新分支时，Git会跟踪“分支”的提交情况，因此它知道所有文件的历史记录。

假设您在master分支上，并且想要创建一个新分支来开发你的网页。 您将执行以下操作：运行<font color="#6495ED">**git checkout -b <我的分支名称>**</font>。 该命令将自动创建一个新分支，并可以在该页面查看，这意味着git会将你移至该分支，脱离master分支。

运行上述命令后，可以使用<font color="#6495ED">**git分支**</font>已创建：

```html
mnelson:myproject mnelson$ git branch
  master
* my-new-branch
```

 [gitbranch.md](https://gist.github.com/cubeton/fa25a25f322a2cd5f405#file-gitbranch-md) hosted with ❤ by [GitHub](https://github.com) 

```html
mnelson:myproject mnelson$ git branch
  master
* my-new-branch
```

 [gitbranch.md](https://gist.github.com/cubeton/fa25a25f322a2cd5f405#file-gitbranch-md) hosted with ❤ by [GitHub](https://github.com) 

分支名称旁边带有星号表示在给定时间指向的分支。

现在，如果您切换回master分支并进行更多提交，则在将这些更改<font color="#6495ED">**合并**</font>到新分支之前，你的新分支将看不到任何更改。

# 步骤六： 在GitHub网页上新建一个仓库

如果只想在本地看到代码，则无需使用网页GitHub。 但是，如果您想团队合作，则可以使用GitHub来协同修改项目代码。

要在GitHub上创建新的仓库，请登录并转到GitHub主页。 您应该看到一个绿色的“ +repository（新仓库）”按钮：

![Git_101_Screenshot1-2](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot1-2-1577239537628.webp)



单击按钮后，GitHub将要求您命名您的存储库并提供简短描述：

![Git_101_Screenshot_2-1](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot_2-1.webp)

填写完信息后，按“创建仓库”按钮创建新仓库。

GitHub会询问您是否要从头开始创建新的存储库，或者是否要添加在本地创建的存储库。 在这种情况下，由于我们已经在本地创建了新的存储库，因此我们希望将其推送到GitHub上，因此请遵循“ **....或从命令行推送现有存储库”部分：**

```html
mnelson:myproject mnelson$ git remote add origin https://github.com/cubeton/mynewrepository.git
mnelson:myproject mnelson$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 263 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/cubeton/mynewrepository.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

```html
addgithub.md hosted with ❤ by GitHub
```

```html
mnelson:myproject mnelson$ git remote add origin https://github.com/cubeton/mynewrepository.git
mnelson:myproject mnelson$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 263 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/cubeton/mynewrepository.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

```html
addgithub.md hosted with ❤ by GitHub
```

（由于您的GitHub用户名和存储库名称不同，因此您需要将第一个命令行中的URL更改为本节中GitHub列出的内容。）

# 步骤七：将分支推送到GitHub

现在，我们将分支中的提交**推送到**新的GitHub存储库。 这使其他人可以看到您所做的更改。 如果它们是由存储库所有者批准的，则可以将更改合并到主（master）分支中。

要将更改推送到GitHub上的新分支，您需要运行<font color="#6495ED">**git push origin**</font>**您的分支名称**。 GitHub将在远程存储库上自动为您创建分支：

```html
mnelson:myproject mnelson$ git push origin my-new-branch
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 313 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/cubeton/mynewrepository.git
 * [new branch]      my-new-branch -> my-new-branch
```

```
addgithub.md hosted with ❤ by GitHub
```

```
mnelson:myproject mnelson$ git push origin my-new-branch
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 313 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/cubeton/mynewrepository.git
 * [new branch]      my-new-branch -> my-new-branch
```

```html
addgithub.md hosted with ❤ by GitHub
```

您可能想知道上面命令中“起源”一词的含义。 当您将远程存储库克隆到本地计算机时，git为您创建了一个**别名**。 在几乎所有情况下，此别名都称为<font color="#6495ED">**“来源”**</font>。它实质上是远程存储库URL的简写。 因此，要将更改推送到远程存储库，可以使用以下命令：**git push git@github.com：git / git.git yourbranchname或git push origin yourbranchname**

（如果这是您第一次在本地使用GitHub，可能会提示您使用GitHub用户名和密码登录。）

刷新GitHub页面后，您会看到注释，说您的名字的分支刚刚被推送到存储库中。 您也可以单击“分支”链接以查看此处列出的分支。

![Git_101_Screenshot1-2](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot1-2.webp)

现在，单击上方屏幕快照中的绿色按钮。 我们将提出合并请求！

# 步骤八：创建合并请求

合并请求（或PR）是一种提醒仓库所有者您想要更改其代码的命令。仓库所有者在检查代码，并确保代码看起来合适后，可将内容更改后放入主分支。
这是提交PR页之前的样子：

提交PR请求后的样子：

您可能会在底部看到一个绿色的大按钮，上面显示“合并拉取请求”。点击这意味着您将您的更改合并到主分支中。
请注意，此按钮并非总是绿色。在某些情况下，它会是灰色的，这意味着您将面临“合并冲突”。 这是当一个文件中的更改与另一个文件中的更改冲突并且git无法确定要使用哪个版本时。您必须手动输入并让git知道使用的哪个版本。
有时，您将成为repo的共同所有者或唯一所有者，在这种情况下，您可能无需创建PR来合并您的更改。但是，创建一个分支仍是一个好主意，这样您可以保留更完整的更新历史记录并确保在进行更改时始终创建一个新分支。

这是提交合并请求页之前的样子：

![Git_101_Screenshot_4](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot_4.webp)

 

提交合并请求后的样子：

![Git_101_Screenshot_5](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot_5.webp)

您可能会在底部看到一个绿色的大按钮，上面显示“合并请求”。点击它意味着您将您的更改合并到主分支中。

请注意，此按钮并非总是绿色。在某些情况下，它会是灰色的，这意味着将出现**“合并冲突”。** 这是当一个文件中的更改与另一个文件中的更改冲突并且git无法确定要使用哪个版本时会出现的情况。您必须手动输入并告诉git使用哪个版本。

有时，您可能是同一个仓库的共同所有者或唯一所有者，在这种情况下，您可能无需创建PR来合并您的更改。但是，创建一个分支仍然是一个好主意，这样您可以保留更完整的更新历史记录并确保在进行更改时始终创建一个新分支。

#  步骤九：同意合并请求

![Git_101_Screenshot_6](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot_6.webp)

完成后，建议您删除分支（太多分支会变得凌乱），因此也请点击灰色的“删除分支”按钮。
您可以通过单击新存储库首页上的“提交”链接来仔细检查提交是否已合并。

![Git_101_Screenshot_7](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot_7.webp)

这将显示该分支中所有提交的列表。你就可以看到刚刚合并的那个（合并请求2）。

![Git_101_Screenshot_8](C:/Users/ASUS/Documents/GitHub/2019-CQUE-translation-project-management-final-/An%20Intro%20to%20Git%20and%20GitHub%20for%20Beginners%20(Tutorial)_files/Chapter1/assets/Git_101_Screenshot_8.webp)

您还可以看到在右侧提交的<font color="#6495ED">**合并代码**</font>合并代码是该特定提交的唯一标识符。这对于引用特定的提交以及撤消更改很有用（使用<font color="#6495ED">“ **git revert**” </font> <合并代码编号>命令可回到那一步）。



# 步骤十： 将GitHub上的更改同步到您的计算机

现在，GitHub上的仓库看起来与本地计算机上的仓库有所不同。 例如，您在分支中进行的提交并合并到master分支中的提交在本地计算机上的master分支中不存在。

为了获得您或其他人已在GitHub上合并的最新更改，请使用**git pull origin master**命令（在master分支上工作时）。

```html
mnelson:myproject mnelson$ git pull origin master
remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From https://github.com/cubeton/mynewrepository
 * branch            master     -> FETCH_HEAD
   b345d9a..5381b7c  master     -> origin/master
Merge made by the 'recursive' strategy.
 mnelson.txt | 1 +
 1 file changed, 1 insertion(+)
```

```
 pulloriginmaster.md hosted with <font color="#4590a3">❤</font> by GitHub
```

```
mnelson:myproject mnelson$ git pull origin master
remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From https://github.com/cubeton/mynewrepository
 * branch            master     -> FETCH_HEAD
   b345d9a..5381b7c  master     -> origin/master
Merge made by the 'recursive' strategy.
 mnelson.txt | 1 +
 1 file changed, 1 insertion(+)
```

```
pulloriginmaster.md hosted with ❤ by GitHub
```

这将向您显示所有已更改的文件及其更改方式。

现在，我们可以再次使用<font color="#6495ED">**git log**</font>命令查看所有新提交。

（您可能需要将分支切换回master分支。您可以使用**git checkout master**命令来执行此操作。）

```
mnelson:myproject mnelson$ git log
commit 3e270876db0e5ffd3e9bfc5edede89b64b83812c
Merge: 4f1cb17 5381b7c
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Fri Sep 11 17:48:11 2015 -0400

    Merge branch 'master' of https://github.com/cubeton/mynewrepository

commit 4f1cb1798b6e6890da797f98383e6337df577c2a
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Fri Sep 11 17:48:00 2015 -0400

    added a new file

commit 5381b7c53212ca92151c743b4ed7dde07d9be3ce
Merge: b345d9a 1e8dc08
Author: Meghan Nelson <meghan@meghan.net>
Date:   Fri Sep 11 17:43:22 2015 -0400

    Merge pull request #2 from cubeton/my-newbranch
    
    Added some more text to my file

commit 1e8dc0830b4db8c93efd80479ea886264768520c
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Fri Sep 11 17:06:05 2015 -0400

    Added some more text to my file

commit b345d9a25353037afdeaa9fcaf9f330effd157f1
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Thu Sep 10 17:42:15 2015 -0400

    This is my first commit!
```

```
view rawgitlogaftermerge.md hosted with ❤ by GitHub
```

```
mnelson:myproject mnelson$ git log
commit 3e270876db0e5ffd3e9bfc5edede89b64b83812c
Merge: 4f1cb17 5381b7c
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Fri Sep 11 17:48:11 2015 -0400

    Merge branch 'master' of https://github.com/cubeton/mynewrepository

commit 4f1cb1798b6e6890da797f98383e6337df577c2a
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Fri Sep 11 17:48:00 2015 -0400

    added a new file

commit 5381b7c53212ca92151c743b4ed7dde07d9be3ce
Merge: b345d9a 1e8dc08
Author: Meghan Nelson <meghan@meghan.net>
Date:   Fri Sep 11 17:43:22 2015 -0400

    Merge pull request #2 from cubeton/my-newbranch
    
    Added some more text to my file

commit 1e8dc0830b4db8c93efd80479ea886264768520c
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Fri Sep 11 17:06:05 2015 -0400

    Added some more text to my file

commit b345d9a25353037afdeaa9fcaf9f330effd157f1
Author: Meghan Nelson <mnelson@hubspot.com>
Date:   Thu Sep 10 17:42:15 2015 -0400

    This is my first commit!
```

```
gitlogaftermerge.md hosted with ❤ by GitHub
```

# 步骤十一：享受你的git glory之旅

您已经成功进行了合并请求，并将您的代码合并到了master主分支中。 恭喜你！ 如果您想了解更深入一点，请查看<font color="#6495ED">**此Git101文件夹**</font>中的文件，以获取有关使用git和GitHub的更多提示和技巧。

我还建议花一些时间与您的团队一起模拟一个较小的小组项目，就像我们在这里所做的那样。 让您的团队使用您的团队名称创建一个新文件夹，并向其中添加一些带有文本的文件。 然后，尝试将这些更改推送到此远程仓库中。 这样，您的团队就可以开始对最初没有创建的文件进行更改，并使用PR功能进行练习。 并且，使用GitHub上的git blame和git history工具熟悉跟踪文件中进行了哪些更改以及谁进行了这些更改。

您使用git的次数越多，您将越感到它的便利。 （我会坚持使用它。）

![0027c58]() 