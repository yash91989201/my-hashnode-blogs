---
title: "👉 Git and GitHub deep dive for DevOps engineers. (Part - 2)"
seoTitle: "Git and GitHub deep dive for DevOps engineers. (Part - 2)"
seoDescription: "Master advanced Git & GitHub in DevOps deep dive (Part 2): explore concepts, workflow, revert, reset, rebase for efficient collaboration"
datePublished: Mon Jul 24 2023 18:18:04 GMT+0000 (Coordinated Universal Time)
cuid: clkh6y26g000k09l20opybxms
slug: git-and-github-deep-dive-for-devops-engineers-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690222136057/5d574869-5d6e-4a64-b4ac-af502fd6e631.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690222502729/d5836553-137a-413c-9bfd-cb946ae5d902.png
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

## **📍 Introduction:**

Hey there readers! 😊 Let's keep exploring the amazing world of Git and GitHub together in this blog post, where we'll dive into the Git workflow and discover even more awesome features. If you're just starting with Git and GitHub, no worries! Simply follow this link to catch up: [https://yashraj-jaiswal.hashnode.dev/git-and-github-deep-dive-for-devops-engineers-part-1](https://yashraj-jaiswal.hashnode.dev/git-and-github-deep-dive-for-devops-engineers-part-1)

If you're looking to practice git commands, I've got a fantastic website for you to check out. Give it a try and have fun learning: [https://learngitbranching.js.org/](https://learngitbranching.js.org/)

## ✔ Git workflow:

After linking your local repository to a remote repository, you are now prepared to begin working on your project in the main branch.

Whenever you make changes, they reside in your working area; at this point, your files are not yet tracked by Git. To ensure they are tracked, you must add them to Git so that their history can be tracked.

In the following example, you can observe that after adding a file and subsequently checking the status, there are some untracked files present.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690212163711/38b53f14-b56d-4f80-8fa4-cc6c5a8cc10f.png align="center")

The git add command adds new or modified files into the staging area. Now, what is a staging area? The staging area is where files are stored before being committed to the history. Let's add the untracked file to the staging area.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690212211277/f48265d8-eaa5-4f07-ade4-00021f388e9a.png align="center")

Upon checking the status, we can see that there are changes ready to be committed. The dot following the add command simply indicates that all new or modified files should be added to the staging area. If you wish to add a specific file to the staging area, simply include the file name along with its relative path (relative to the current directory), separated by a space.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690212285395/476eb9dc-ef01-4062-aaf3-a7a0c6813f2e.png align="center")

At this point, if we check our git log, we will see that there are no commits, meaning there is no history for our project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690212347385/72f970a7-7b31-4fc1-b275-d8a3d71ad92b.png align="center")

Let's commit our changes by executing the 'git commit' command and providing an appropriate commit message using the '-m' flag.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690212467402/be398662-108c-4a8e-ac90-52bb3183e9e0.png align="center")

Now, when checking the git status, we'll find that there is a commit in our log. This indicates that the changes have been added to our git history.

Now let's push these changes to our remote repository so that everyone can view our changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690213157608/7e0f05e9-6fb1-4ded-ac91-dd53c9acbff1.png align="center")

After pushing our changes to the remote repository using `git push origin main` command, we can see those changes reflected on our GitHub account.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690213328279/7c4803b6-e4f2-4690-ab1e-01ceb0180d71.png align="center")

## ✔ Git revert and reset:

The revert and reset commands are used when we want to remove changes that have been committed to the history. The revert and reset commands function differently to restore the commit history. Let's see how they work.

### 🔸reset command:

The **git reset** command is used to revert to a previous commit, effectively removing all changes made up to that point and returning them to the staging area.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690218806812/89393f7c-c954-48ca-9b50-0fd0583423ca.png align="center")

In the example above, we reset the commits before the `fo8eb..` commit. Now, all the commits before it has been removed and placed in the staging area.

### 🔸 revert command

In git, the revert command can be used in cases where we want to restore to the previous commits but don't want to remove the commit history. When we use the `git revert` command a new commit is created that undoes the changes of the given commit.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690219574827/b0e5e92d-703c-444c-895d-ff97cd358c5e.png align="center")

In the given example, we can observe that the `b3e46..` commit is created by reverting the `3604e..` commit. Unlike the reset example, where the commits following the specified commit were removed, the revert method creates a new commit in which the changes made in the specified commit are undone.

## ✔ Git rebase:

Let's say you are attempting to fix a bug and have multiple commits, each addressing different aspects of the same feature. Now, you want to combine all those commits into one. For this purpose, we can use the rebase command, which allows us to specify the commits that we want to merge into a single commit.

In the following example, let's assume we want to merge commits `8811..`, `e03fe..`, and `be52..` into one. We can use the rebase command and specify commit be9381e. This will open an editor where we can easily select the commits we want to squash into a single commit.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690220346474/b934fac5-963c-4386-8075-4484d3309e10.png align="center")

We can execute the rebase command using `git rebase -i commit_hash` to access an interactive environment where we can easily see and update which commits are being squashed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690222672463/1676e4bb-9fd2-4d6a-8af3-505e844b1124.png align="center")

Whenever "pick" is mentioned, it merges all the commits marked with "squash" below it. In our case, "fix feature on mobile devices" and "fix feature on tablet devices" will be merged into "fix feature on desktop devices."

After closing the editor you will get another tab where you can edit the commit messages

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690221014000/f4d5701c-ad3a-42e7-aac9-5dce036b4f4e.png align="center")

After updating the commit messages and closing the tab your changes will be merged into one commit. Use `git log` command to check. You can also see that a new commit hash is generated ie `f81761..` as opposed to the previous one i.e. `881193..`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690221089986/64d28bc9-d586-4b74-ad20-3a198ec694dc.png align="center")

## **📍 Conclusion:**

In conclusion, we have dived into advanced Git concepts such as git workflow, revert, reset, and rebase. However, there are more advanced commands that can be incredibly useful when understood properly. Don't forget to visit: [https://learngitbranching.js.org/](https://learngitbranching.js.org/) where you can practice git commands. Stay tuned for the next blog, where we will explore additional advanced Git commands.