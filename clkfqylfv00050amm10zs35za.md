---
title: "👉 Git and GitHub deep dive for DevOps engineers. (Part - 1)"
seoTitle: "Git & GitHub: DevOps Engineers' Deep Dive (Pt.1)"
seoDescription: "Master Git & GitHub for DevOps engineers: dive deep into branches, local/remote repositories, and seamless collaboration in Part 1 of our series"
datePublished: Sun Jul 23 2023 18:02:49 GMT+0000 (Coordinated Universal Time)
cuid: clkfqylfv00050amm10zs35za
slug: git-and-github-deep-dive-for-devops-engineers-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690135101937/3cb9af4a-6eaf-4d5b-9960-339734e17ab2.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690135330505/6096d893-c667-4941-8d60-7af213c73521.jpeg
tags: linux, git, devops, 90daysofdevops, trainwithshubham

---

## **📍** Introduction:

Hello readers! In today's blog, we'll be exploring Git and GitHub together. We'll learn how to link our local repository to a remote one hosted on GitHub, making it super easy to share our code with others and collaborate with fellow developers. Exciting, right? Let's dive in!

## ✔ Branches in git: 🫒

In Git a branch is a version of the repository that simply diverges from the main working project. A git repository can have different branches in it. Branches allow us to work on different functionalities of the same project at once, when we create a new branch all the files are copied to that branch from the base branch and all the files that are in the new branch also have the history of the changes.

Here's an example to better your understanding.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690128520882/6333a1bd-1bca-4549-be10-1f66b836944e.png align="center")

Let's suppose our repository has a main branch containing the source code and all ongoing changes. If we need to implement a new feature, we can create a new branch from the main branch (Feature 1). Keep in mind that development in the main branch can continue even after creating a new branch. If we need to add a crucial feature to our project, we can create another branch (Important Feature) from the main branch and continue working on the main branch.

Observe that we now have two distinct branches originating from the main branch. Once the work on the Feature 1 branch is complete, we can merge it back into the main branch. Similarly, we can merge the Important Feature branch into the main branch after completing the work on it.

## ✔ Difference between main branch and master branch.

There is no significant difference between the main branch and the master branch. Previously, the primary branch in Git was referred to as the master branch, but due to a change in convention, it has been renamed to the main branch.

You can change the name of the primary branch in your local repository using the following command: `git branch -m master main`. This specifies the current primary branch's name and then the new name for the primary branch.

## ✔ Creating a new repository on GitHub.

It is very easy to create a new repository on GitHub,

1. Visit the GitHub website and log in to your account. Next, click on the "New" button in the left panel.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690130210781/710ee5fa-9646-46bd-bdca-722fb70c3c15.png align="center")
    
2. Enter the details of your repository, such as the name you want to give it and a short description. Then, click on the "Create Repository" button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690130406592/b395e841-5214-4b77-9cc8-22e7fe7c4ce7.png align="center")
    
3. After creating a new repository on GitHub, you will be directed to the following page. The steps below explain how to connect your local repository to the remote repository you just created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690130456992/a75814a1-59e3-4c3f-9c6c-4b7a17cae9d1.png align="center")
    

## ✔ Difference between local repository and remote repository.

The local repository is a Git folder on your computer. The remote repository is a Git folder on another computer.

Remote repositories are used by teams to share changes from their local folders. When you're done making changes, you can save them to your local repository without the internet. No one else can see these changes and when you want to share the changes, you can send them from your local repository to the remote repository.

## ✔ Connecting local repository to remote repository. 🔗

To create a new local repository and connect it to the remote repository that we just created now follow the following steps:

1. `git init`: this will initialize a new git repository in your local machine.
    
2. `echo "# test repository" > README.md`: Here, we create a file that can be pushed to the remote repository.
    
3. `git status`: With the help of this command, we can view newly added files in the local repository and any modified files. In the example below, we can see that after adding "README.md," it appears as a new file.
    
4. `git commit`: After the changes have been added, we can commit them and include a commit message that explains the modifications in detail. When we commit our changes, a snapshot of all the changes is taken.
    
5. `git branch -M main`: We then change the primary branch name to "main" since it is also the primary branch in the remote repository.
    
6. `git remote add origin`: Here, we add the URL of the remote repository, thereby enabling us to push the changes.
    
7. `git remote -v`: This command helps us view the remote repository connected to our local repository.
    
8. `git push origin main`: After changes have been committed, we can push these to the remote repository, allowing everyone to view our updates.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690132790297/2fb6b9fb-d1cb-4e2f-8e60-1455d1a284d6.png align="center")

After pushing the changes, refresh the GitHub page. Now, you can see the files you have pushed are reflected in the remote repository.

## **📍** Conclusion:

In conclusion, Git and GitHub are essential tools for DevOps engineers that facilitate collaboration and version control. Understanding branches, local and remote repositories, and connecting them enables seamless sharing and managing of code. By mastering these concepts, engineers can effectively contribute to and manage projects in a collaborative environment.