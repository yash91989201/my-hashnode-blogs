---
title: "👉👑 Advanced Git and GitHub for DevOps engineers.🔥🔥"
seoDescription: "Master Git commands for DevOps, manage branching, resolve conflicts, maintain history, and optimize workflows"
datePublished: Tue Jul 25 2023 18:27:19 GMT+0000 (Coordinated Universal Time)
cuid: clkimpsoc000009i4c6dlgauz
slug: advanced-git-and-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690307511125/e24c3968-edf3-4d12-bbda-aa599320fd96.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690309604493/5ba2ab24-5868-4f17-bf9d-6710e46bb282.png
tags: git, devops, 90daysofdevops, trainwithshubham, advanced-git-and-github

---

## **📍** Introduction: 👨‍🏫

Hey there! In this article, we're going to explore some super handy and flexible Git commands. By learning these advanced features, you'll be all set to manage complex branching strategies, sort out conflicts like a pro, and keep your commit history neat. So, let's jump in and discover commands that will make you the DevOps engineer that you have always wanted to be!

## ✔ Using git merge and rebase: ⚙️

When working with multiple branches in Git, it's crucial to incorporate all your changes into the main branch. For this, there are two commands available: **rebase** and **merge**. Both combine the work of multiple developers into a single entity, integrating changes between branches.

### 🔸 Git merge: ⛙

While working on a new feature in the main branch, you decide to create a separate branch. After finishing working on the feature you want to merge your work into the main branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690301033392/d2843616-85d6-4ea1-8f15-5d6f69538d9a.png align="center")

If you want to merge the main branch into the feature branch, first "checkout" to the main branch (i.e., the branch from which changes will be merged). Then, execute git merge feature, and the commits from the main branch will be merged into the feature branch. This will also create a new commit just for the merge. Also after merging, you can see the complete history of commit merging.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690301299960/45edd843-96e2-4c28-9d7c-3b6dc11d3a53.png align="center")

### 🔸 Git rebase: ⏫

Rebasing is the process of altering the base of your branch from one commit to another, giving the impression that you created your branch from a different commit. rebase is used when we want to achieve a linear git history.

Let's consider the following scenario: you create a new branch from the main branch to work on a new feature. As you develop the feature, you notice that the main branch has new commits. Now, you want to incorporate those changes into your branch. Here we can use the rebase command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690304882435/1eba0316-880d-4e94-89b4-ca88e902419a.png align="center")

In the above image, we can see that after rebasing it seems that the feature branched was started from the point where the new commits have been added in the main.

You must never use rebase on a remote repository as it removes the history of commits making it hard to track the changes.

## ✔ Difference between rebase and merge: 📋

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>merge</strong></p></td><td colspan="1" rowspan="1"><p><strong>rebase</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p>Merge lets you merge different Git branches.</p></td><td colspan="1" rowspan="1"><p>Rebase allows you to integrate the changes from one branch into another.</p></td></tr><tr><td colspan="1" rowspan="1"><p>Merge logs show you the complete history of commit merging.</p></td><td colspan="1" rowspan="1"><p>Rebase logs are linear. As the commits are rebased, the history is altered to reflect this.</p></td></tr><tr><td colspan="1" rowspan="1"><p>All the commits on a feature branch are combined into a single commit on the master branch.</p></td><td colspan="1" rowspan="1"><p>All commits are rebased, and the same number of commits are added to the master branch.</p></td></tr><tr><td colspan="1" rowspan="1"><p>Merge is best used when the target branch is supposed to be shared.</p></td><td colspan="1" rowspan="1"><p>Rebase is best used when the target branch is private.</p></td></tr><tr><td colspan="1" rowspan="1"><p>Merge preserves history.</p></td><td colspan="1" rowspan="1"><p>Rebase rewrites history.</p></td></tr></tbody></table>

## ✔Merge conflicts: ⚔️

A merge conflict occurs when Git cannot automatically resolve differences in code between two commits. Git can merge the changes automatically only if the commits are on separate lines or branches.

In the following example, when merging two branches, namely master and dev, a conflict arises due to differing lines of code on the same line in both branches. While resolving commits in Visual Studio Code, an editor is provided where we can select which changes to incorporate in the final commit.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690305894938/bf27efa6-9216-4189-99af-6c36ad28c7cd.png align="center")

Here, I have combined both changes, prioritizing the current changes since I am currently checked out in the main branch. This way, the new feature is also added, but the hotfix and bug fixes that were completed in the master branch are all available in the master branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690306118109/f0879aa2-00af-462d-9a4a-c749ad1f43a3.png align="center")

Here we can see this visually, now the master branch has the new feature code as well as the bug fix and hot fix made on the master branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690306239437/c79f41fa-cd2c-4091-966d-b48a7971d3b9.png align="center")

## ✔ Git stash: 💾

While working on a feature, if we want to test something new without losing our current work, we can use the stash command. This command saves our changes and lets us use them again later if we want to.

In the example below, we have made some modifications to the index.js file. However, if we want to make new changes with a clean slate, we can use the git stash command.

After executing git stash and checking the status, we'll see that the staged changes have disappeared. By examining the output of the git stash command, we can confirm that it has saved the working directory in the stash.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690306760564/5642e0b5-0e24-428d-8706-7bbbc43611c1.png align="center")

To retrieve our stashed changes, simply execute `git stash pop`. This will take the most recent stash and place it in our working directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690307017000/936f84f6-0520-4279-8541-685cd50c381e.png align="center")

## ✔ Cherry Pick : 🍒

Git cherry-pick is a powerful command that allows you to select specific Git commits by reference and append them to the current working HEAD. Cherry-picking involves choosing a commit from one branch and applying it to another.

Let's an example where there are two branches ie master and feature01-bugFix. The bug fix branch contains multiple commits.

\*master branch

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690308314496/95e8a6a3-2cd1-4092-a8c7-e9a0d3a14326.png align="center")

\*feature01-bugFix branch

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690308340151/b62394c5-875b-435b-bd3d-ed849ca2bfa1.png align="center")

Now we can use the cherry-pick command to get all those commits into the master branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690308548634/7db67f5b-4651-4243-9b21-a3b6a18bcf74.png align="center")

After executing the cherry-pick command we will get a merge conflict as the master branch has some work that feature01-bugFix does not have.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690308510073/fe1da34f-c456-4e73-9c3e-7aa51ec08416.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690308518958/9145e86b-be81-47d6-aa15-35ac94e9c2b5.png align="center")

Git cherry-pick is a useful tool, but it's not always the best practice. Cherry-picking can lead to duplicate commits, and in many situations where cherry-picking would be effective, traditional merges are preferred.

## **📍** Conclusion:

Hey there! You've now become a Git whiz by learning awesome commands like merge, rebase, stash, and cherry-picking. Keep practicing them and you'll soon feel super confident using them in real-life situations. Happy learning!