---
title: "Fundamentals of  Git and GitHub Skills for DevOps Engineers 🛠️"
seoTitle: "Git & GitHub Basics for DevOps Engineers"
seoDescription: "Master Git & GitHub essentials for DevOps: enhance collaboration, version control, project management, and elevate software development skills"
datePublished: Sat Jul 22 2023 15:35:43 GMT+0000 (Coordinated Universal Time)
cuid: clke69kwa000b09ms5wf5b8mt
slug: fundamentals-of-git-and-github-skills-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690040111574/232a60d9-4c5c-40d7-bb78-1db594fbe328.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690040120786/52ffc318-47c4-4074-be4f-0b0e93e2acc2.jpeg
tags: git, devops, learning-journey, 90daysofdevops, trainwithshubham

---

![Centralized vs Distributed Version Control System](https://www.htown-tech.com/uploads/6/9/4/9/69493533/centralized-vs-distributed-version-control-system-1_orig.jpg align="left")

## **📍** Introduction:

Hello everyone! In today's blog, we'll explore Git, a popular DevOps tool, and GitHub, a service that utilizes Git. These tools are essential for DevOps engineers as they streamline collaboration and version control in software development.

## ✔ Version Control System ⚙️:

A version control system is used to track all the changes in the code base and keep all the history in one place, such as when a file was created and which lines of the file were changed, when, and by whom. All these changes made to a file or folder are stored as a version in this system and become very helpful when we want to restore the file to its previous version.

There are two main types of version control systems:

1. **Centralized Version Control System (CVCS):** A CVCS is designed such that all versions of a project file are stored on a central server. If a developer wants to make changes to the code base, they "check out" the files from the central server, after making the desired changes the developer then "checks in" the updated files to the central server. Examples of CVCS include Subversion and Perforce.
    
2. **Distributed Version Control System (DVCS):** A DVCS works in such a way that it allows developers to clone the entire project, along with all of its version history, onto their local machines. Cloning the entire repository onto their machines enables developers to make any changes they want in the code base and then later merge those changes into the main repository. Examples of DVCS include Git, Mercurial, and Darcs.
    

### 🔸 Advantages of DVCS over CVCS: 🔥

Some advantages of DVCS over CVCS include:

1. Faster operations since most actions are performed locally.
    
2. Allows offline work, as the entire repository is cloned on the developer's machine.
    
3. Enhanced collaboration, as each developer, has a full copy of the repository.
    
4. Improved data redundancy, as every developer's machine acts as a backup.
    
5. Easier branching and merging, promoting experimentation and feature development.
    

## ✔ What is Git? 🤓

![How to install Git on Android with Termux (Step-by-Step Guide)](https://www.techrepublic.com/wp-content/uploads/2017/10/git-logo.jpg align="left")

Git is an open-source, <mark>distributed version control system</mark> that's perfect for handling projects of any size, quickly and efficiently. It's made to make life easier for developers, helping them keep track of and collaborate with their teammates in the same workspace. Thanks to Git, working together on projects and managing them becomes a breeze!

Git serves as the foundation for many services, such as GitHub and GitLab, but it can be used independently of these platforms. Both private and public use of Git is possible. Created by **Linus Torvalds** in 2005 for the development of the Linux Kernel, Git has become a crucial distributed version control tool in the DevOps field. With its ease of learning and fast performance, Git surpasses other SCM tools like Subversion, CVS, Perforce, and ClearCase.

### 🔸 Basic git commands:

1. `git init`: The git init command is utilized to establish a local git repository. This action generates a .git folder containing all the necessary files for managing file history.
    
2. `git add`: The git add command incorporates the modifications made to the source code into a staging area. These changes can then be committed to the code.
    
3. `git commit`: The git commit command commits the updated code, and a commit message must accompany it. This message explains all the changes included in the commit. To provide the commit message, use the -m flag, like this: `git commit -m`.
    
4. `git push`: After creating a commit, we need to push the changes to an online repository, such as GitHub, so that the newly made updates are reflected in the repository and accessible to everyone.
    

## ✔What is GitHub?

![Integrating Github With Eclipse - YouTube](https://i.ytimg.com/vi/ptK9-CNms98/maxresdefault.jpg align="left")

GitHub is a website that hosts Git repositories and has a user-friendly interface. It's the biggest coding community in the world. When you upload code or a project to GitHub, more people can see it. Programmers can find code in different languages and use Git to make and follow changes.

GitHub helps team members work together on a project from anywhere, making it easier to collaborate. It also lets users look at older versions of their work.

## **📍** Conclusion:

In conclusion, Git and GitHub are essential tools for DevOps engineers, providing efficient version control and collaboration capabilities. Together, these tools streamline software development and project management, making them indispensable for DevOps professionals.