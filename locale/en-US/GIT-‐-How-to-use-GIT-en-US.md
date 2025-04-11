# How to use Git

The operation structure of the git is illustrated as follows.

![git work](https://i.namu.wiki/i/mGOcwPPFpufxXoG8aekOcDTHkqQuB85P0FbGyo20byibTjAXSomWr5KRYYq4-vLUJa9-Ido0iN0vYppj8TGdk8n5WsTARe2R9mNsAJMwzjA2k1Nq-nueN5djnybzvchX0-vgokH8x5pUYa5rJO4PSg.webp)

**A three-line summary..**

1. Save the work change history in local repository.(add, commit)
2. Make a synchronization request to the remote repository for the work history in the local repository.(push)
3. Get the latest change history when synchronization is complete.(pull)

- **Repository**: This is where all the files and changes in the project are stored.
- **Commit**: In units that store snapshots of files, record changes.
- **Branch**: A branch point where you can work independently. The default branch is 'main' or 'master'.
- **Staging Area**: A space where temporarily store files to be commits.
- **Remote Repository**: A repository accessible through a network, primarily used for collaboration.

## Create Local Repository


How to create a local repository.

1. Open the terminal in vscode.

2. Enter `git init` and run it. It's over.

```
D:\my-test\nodejs-guide> git init
Initialized empty Git repository in D:/my-test/nodejs-guide/.git/
```

Message will appearance that git repository is created.

When you go to project folder you can find the .git folder.

![image](https://github.com/user-attachments/assets/d48ad321-8105-4a87-bd37-a34f1cb8733f)

Local git repository is separated in 3 area.

1. Working Directory
2. Index
3. HEAD

**Working Directory** is made up of real files.

**Index** is staging area.

**HEAD** is the latest commit area.


First, add (add) the changed file to the index.

Commit records changes to all files in the folder you are currently working on in your local repository.

### Create gitignore

There's a problem here: node_modules has a huge amount of packages installed, which is too large to store together in git.

You also need a gitignore file to prevent items like hidden files that need to be kept confidential from being saved in git.

Create `.gitignore` file in explorer


You can also enter it yourself, but there are also sites that make it easy to create.

Link => https://www.toptal.com/developers/gitignore

Enter the operating system, development environment, language, or tool and click the Create button to create .gitignore content 

![image](https://github.com/user-attachments/assets/5f50a94d-0b4c-4656-8d91-9d584c39efa5)

Copy & paste contents.


```
# Created by https://www.toptal.com/developers/gitignore/api/windows,visualstudiocode,node
# Edit at https://www.toptal.com/developers/gitignore?templates=windows,visualstudiocode,node

### Node ###
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
lerna-debug.log*
.pnpm-debug.log*

... It's too long, so I'll skip it.

```

## Check git status

Git automatically detects when a file is added for the first time or its contents changed.

You can check it with the terminal command, but I will explain it focusing on the vs code screen.

### add

If you look to the left side of the vs code, you will see the Source Control tab. Click to see the Source Control screen.

The changes show a list of files that have changed. 

You need to add them all because no files are registered when you set the git for the first time.

When you mouse over the changes, + appears, and you can add them in batches, and you can add them individually.

![image](https://github.com/user-attachments/assets/ebf1eaac-b29f-4eba-a049-26806539cd50)

You can see that the items in the changes have been moved to the staged changes.

![image](https://github.com/user-attachments/assets/f5cd7bba-a64c-4690-851d-3348cea65651)

### commit

Commit the files in the staging entry.

Commit is saved staging file's snapshot in local repository. 

Commit leaves a history of change, and plays an important role in returning to a certain point in time or collaborating with others.

When committing, it is easy to check what I did through a message, so it is recommended to leave a message.

Rule of messaging.

```
Type(scope): Topic(title) // Header

text // Body

Footer // Footer
```

**Header** is required and scope is optional.

The type is a label that indicates what commit is about.

Among the items below, the most frequently used items are feat, fix, and docs.


| 타입 이름    | 내용                                                            |
|----------|---------------------------------------------------------------|
| feat     | Commit to new features                                        |
| fix      | Commit to bug fix                                             |
| build    | Commit to build file / Commit to install or build file change |
| chore    | Commit to etc modify                                          |
| ci       | Commit to ci setting modify                                   |
| docs     | Commit to document modification                               |
| style    | Commit to code style or format                                |
| refactor | Commit to code refectoring                                    |
| test     | Commit to test code modify                                    |
| perf     | Commit to performance improvement                             |

**Body** is a writes down details that support the content of the Header.

You can skip it if the header is sufficiently explainable.

**Footer** is used to add reference information from an issue.

Footer also can skip.

Let's practice in vscode.

Enter the `feat: first commit` in message area.

![image](https://github.com/user-attachments/assets/ed1bb02c-b122-4e62-a1aa-869c5c74de51)

Click the commit button right arrow here to see the option.

![image](https://github.com/user-attachments/assets/e09b0b45-98c8-4be2-82a5-de15d84298fa)

Commit is to store in the local repository, and commit and push is to store in the local repository and request synchronization to the remote repository.

First, start with commit and explain the remote repository later.

When you commit, the contents of the commit are recorded in the source control graph and the repository tab.

![image](https://github.com/user-attachments/assets/53c80621-68a7-405e-820e-9bbc5bb49ae7)

## Remote repository

### GitHub

GitHub is a web service based on git, a platform to manage and collaborate on projects. 

In addition to github, there are GitLab, Bitbucket, SorceForge, Azure DevOps Repos, etc.

The repository is a project repository, and it is stored in the repository when git push is performed.

### Setting remote
It's easy to add a remote repository in vscode.

Click '...' in Source Control > Remote > Remote Add.

When the top of the screen input window appears, enter the github address.

https://github.com/pmirnc-dev/pds-welcome.git

![image](https://github.com/user-attachments/assets/0625661e-5019-4b46-bde7-23607192ccc7)

It says to enter a remote name, but by default, you can enter origin.

![image](https://github.com/user-attachments/assets/c8c443a9-d853-47fa-9aed-4b5c97d9ec88)

### push

If the connection is successful, you can verify that Remote Repository is connected to Remotes as origin.

![image](https://github.com/user-attachments/assets/6cea1a21-e4cf-4f49-8045-d2ca059521b4)

Click the publish branch button to save the work to a remote repository.

![image](https://github.com/user-attachments/assets/4af36ff2-340b-4512-a309-b0c9417fdef0)

## Collaborating

If you do the project alone, it doesn't matter how you use the branch.

However, if you work as a team, you may experience problems such as accidentally modifying or deleting the code that other Sarim worked on.

To prevent this, we will find out how to collaborate.

### clone

Project manager will create a remote repository.

Project copy remote repository in the local project.

You must copy it to a local project with a remote git url address.

Move to the folder where you want to create the project.

![image](https://github.com/user-attachments/assets/b65f57eb-237c-4657-a757-8824127389f1)

In the folder, right-click anywhere > Open Git Bash here.

The Terminal window appears, and to copy the project, use the following commands.
```
git clone https://github.com/pmirnc-dev/pds-welcome.git
```

![image](https://github.com/user-attachments/assets/654c88c0-0a3d-4ffe-acbe-2e3340d34186)

If the project copy is successful, you can verify that a folder has been created with the remote repository name in the navigator.

![image](https://github.com/user-attachments/assets/4f45d7d3-bf99-4a01-a0d2-5a66099902a6)

Open the new project using vscode.

Select File > Folder Open, and open the new project folder.

### branch

Let's give an example.

There is an error in the code that looks up the bulletin board and needs to be corrected.

You can modify the main branch directly, but you need to separate the work area because it may overlap with other team members.

What you need at this time is a create branch.

1. main branch right click -> Create branch

![image](https://github.com/user-attachments/assets/4a4199dd-01d0-4338-b9fc-6224cadf5a50)

2. Enter brach name

There are two branch naming conventions used by PMI.

    1. User Initial/Work Name
    2. #issue number-work name

![image](https://github.com/user-attachments/assets/dcdde509-a108-43ba-b8fa-0b72a8ec84bb)

3. There are three options. Create & Switch to Branch will take you to branch properties and newly created branches.

![image](https://github.com/user-attachments/assets/cbb67fef-91bb-457e-a87c-b87aa7479279)

4. New created branch

![image](https://github.com/user-attachments/assets/40b21ba2-fa87-43bb-99f7-64e70e6a3de9)

## Pull Request(PR)

You must now merge the modifications made in the job branch into the master branch.

Pull Request is a feature that allows developers to review their work to other team members and ask them to merge.

Push the work from ihwang/branch_test to a remote repository.

Push creates a yellow space in the github and click the Compare & pull request button.

![image](https://github.com/user-attachments/assets/0eff2c5d-d1cd-44fc-9543-7f3a363ef553)

As you go to the Open pull request screen, you can add a description of my work, and the changes are shown at the bottom.

![image](https://github.com/user-attachments/assets/993cda2c-ecb9-46da-94a5-613c383cbea9)

When you click the Create pull request button, Github automatically checks the conflict.

![image](https://github.com/user-attachments/assets/f3b2ed13-0c77-487f-9445-25dd1ab258eb)

If the work is fine, click the Merge pull request button to merge the ihwang/branch_test into the master branch.

![image](https://github.com/user-attachments/assets/8377e8aa-011e-432d-9492-9f5fb28004af)

When mridge is completed, it will change to Merged state in purple, and there will also be a branch deletion.

If you're not going to use it anymore, delete it neatly and just leave it to continue working.

![image](https://github.com/user-attachments/assets/9189014d-9611-479f-8a24-a3e7269f2d6a)

## Pull

The state of the master branch changes because the new changes have been merged into the master branch

The master also needs synchronization, so check out with the master branch.

![image](https://github.com/user-attachments/assets/8a620a8f-bfbf-49b0-8025-d8fcbccbf3bd)

Synchronizing changes also creates index.html, main.js in the master.

![image](https://github.com/user-attachments/assets/0f284ee9-01e7-49ed-840f-c0ab32abb17c)

## Conflict
Sometimes when I'm working on it, fixing the same code and merging branches can cause conflicts.

The first time you experience it, it's very embarrassing, so you don't have to worry. (The importance of division of work and communication)


To reenact the crash situation, we will first modify one line of code from master to main.js and proceed to push.

Then go to a different branch and modify the same part with a different code.

![image](https://github.com/user-attachments/assets/4561bd78-7b7d-461b-80b8-cd5cbd0eacda)

You can see that the message Conflict appears differently from the previous one.

![image](https://github.com/user-attachments/assets/ddc2225b-2921-4311-95aa-15a2442d663b)

Click Resolve conflicts to confirm.

![image](https://github.com/user-attachments/assets/7a638456-2cad-41a3-aaf8-ace50f92384c)

======= Based on , the top is ihwang/branch_test and the bottom is master.

Feel free to edit the code that will eventually be left.

If you make a correction and click Mark as resolved to the right, it turns into commit merge.

![image](https://github.com/user-attachments/assets/bd494dfa-4d5d-4b20-b295-e666bfbefcc2)

You passed the conflict test and you can do Merge.

![image](https://github.com/user-attachments/assets/894daca9-c5c8-4585-93d2-d2f5131972e8)

