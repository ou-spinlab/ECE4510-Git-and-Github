# Git and GitHub

## Overview

Git is a version control system used to track changes to files. GitHub is an online service for hosting Git repositories.

In this assignment, you will set up Git and GitHub, create your own copy of this repository, make and commit changes, push those changes to GitHub, create a branch, and resolve a simple merge conflict.

The Git commands used in this assignment are the same on Windows, macOS, and Linux. On Windows, you can use PowerShell. On macOS or Linux, you can use a terminal.

> **Note:** For this assignment, you should use the command line for Git operations, but you may use the Git tools built into your text editor or IDE for future assignments.

## Resources

If you are new to Git, you may find the following resources helpful:

* A [4-minute high-level explanation of Git](https://www.youtube.com/watch?v=e9lnsKot_SQ).
* The [Pro Git](https://git-scm.com/book/en/v2) book provides a comprehensive overview of Git. I suggest using it primarily as a reference rather than reading it cover to cover. The following sections are particularly useful:

  * [Getting a Git Repository](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository)
  * [Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
  * [Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)
  * [Undoing Things](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)
  * [Working with Remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
  * [Branches in a Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
  * [Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* GitHub's guide for [Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).
* As you become more familiar with Git, [Oh Shit, Git!?!](https://ohshitgit.com/) is a useful reference for recovering from common mistakes.

## 1. Create a GitHub Account

If you do not already have a GitHub account, create one at: https://github.com/. You will use this account to host Git repositories throughout the course.

## 2. Install Git

Install Git on your computer: https://git-scm.com/downloads. Git is available for Windows, macOS, and Linux. After installation, open a terminal and verify that Git is installed:

```console
git --version
```

You should see the installed version of Git.

## 3. Configure Git

Git associates your name and email address with the commits that you create (more on commits later in the assignment). To have your commits associated with your GitHub account, use an email address associated with your GitHub account.

Configure these before continuing:

```console
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

> **Note:** If you prefer not to expose your personal email address in your Git commit history, GitHub provides a `noreply` email address that you can use instead. You can find this address in your GitHub email settings. Personally, I do not use the `noreply` email address, but the option exists if this is important to you.

You can check your configuration by running the same commands without arguments:

```console
git config --global user.name
git config --global user.email
```

You only need to perform this configuration once on each computer. Git can also be configured to use different names and email addresses for different repositories, but this is beyond the scope of this assignment.

## 4. Configure SSH Access to GitHub

GitHub needs to authenticate your computer before you can push changes to a repository. For this course, we will use SSH authentication.

> **Note:** GitHub also supports HTTPS, but GitHub no longer allows account passwords to be used for Git authentication over HTTPS. Password authentication was discontinued in 2021; HTTPS now requires another authentication method, such as a personal access token.

First, check whether you already have an SSH key. If you do not, follow GitHub's instructions to generate one and add it to your GitHub account. The instructions are provided separately for Windows, macOS, and Linux:

[Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

After configuring your SSH key, test the connection:

```console
ssh -T git@github.com
```

The first time you connect, you may be asked whether you trust the connection. You can answer yes to this prompt. A successful connection should display a message similar to the following:

```console
Hi YOUR_GITHUB_USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

> **Important:** Your private SSH key should never be shared with anyone or uploaded to GitHub.

## 5. Fork the Assignment Repository

The repository for this assignment is:

https://github.com/ou-spinlab/ECE4510-Git-and-Github

A fork creates your own GitHub copy of an existing repository.

1. Open the assignment repository on GitHub.
2. Click "Fork" near the upper-right corner of the page.
3. Select your personal GitHub account as the owner.
4. Create the fork.

You should now have your own copy of the repository under your GitHub account. For example, your repository will be located at:

```text
https://github.com/YOUR_GITHUB_USERNAME/ECE4510-Git-and-Github
```

## 6. Clone Your Repository

A repository stored on GitHub is called a **remote repository**. To work with the repository on your computer, you first need to clone it. You can do this by opening a terminal and navigating to the directory where you want to store your coursework.

Clone your fork of the repository using SSH (replacing `YOUR_GITHUB_USERNAME` with your GitHub username):

```console
git clone git@github.com:YOUR_GITHUB_USERNAME/ECE4510-Git-and-Github.git
```

You can also copy this URL by clicking `Code` on your fork on GitHub and selecting `SSH`.

Now, you can move into the local copy of the repository:

```console
cd ECE4510-Git-and-Github
```

You can view the URLs of the remote repositories associated with your local repository using:

```console
git remote -v
```

You should see your GitHub repository listed as `origin` for both fetching and pushing.

> **Important:** `git clone` is used when downloading a repository for the first time. Once you already have a copy on your computer, `git pull` can be used to retrieve new changes from the remote repository.

## 7. Make Your First Change

Create a file called `student.txt` and add the following using your favorite text editor:

```text
Name: Rick Sanchez
GitHub username: ricksanchezj22
Email: ricksanchez@j22.example
```

Save the file.

For now, leave the contents exactly as shown. Later in the assignment, you will create a branch and correct this information to use your own information.

Git should now recognize that a new file has been created, but the file is not yet being tracked. You can check the status of your repository with the following command:

```console
git status
```

You should see `student.txt` listed as an untracked file.

## 8. Stage and Commit Your Change

Before Git records changes in the repository history, you first **stage** the changes that you want to include. Staging allows you to select which changes will be included in the next commit. A **commit** records the staged changes as a snapshot in the repository history.

Stage the file:

```console
git add student.txt
```

Check the repository again:

```console
git status
```

Now, you will see the file listed under the changes to be committed.

Commit the file (with a brief message describing the commit):

```console
git commit -m "add student.txt"
```

Inspect the commit history:

```console
git log
```

You should see the commit that you just created.

> **Note:** Depending on your terminal, `git log` may open in a scrollable viewer. Press `q` to exit and return to the command line.

A more compact view of the history can be displayed using:

```console
git log --oneline
```

## 9. Push Your Commit to GitHub

Your commit currently exists only in the local repository on your computer. To update the remote repository, you can push your changes to GitHub:

```console
git push origin main
```

In this command:

* `origin` is the default name for the remote repository that you cloned. A repository can have multiple remotes, but the primary remote is typically called `origin`.
* `main` is the name of the primary branch in the repository. We will discuss branches in the next section.

> **Note:** GitHub historically used `master` as the default name for the primary branch. In 2020, GitHub changed the default branch name for new repositories to `main`. There are still many repositories that use `master` as the name of the primary branch.

After pushing, open your repository on GitHub in a browser and verify that your changes appear there. At this point, your local repository and your repository on GitHub contain the same changes. If you push again without making any new commits, Git will report that everything is already up to date.

## 10. Create a Branch

Branches allow you to work on changes independently from the main version of a project.

For example, consider that you are working on a project with a team and want to implement a new feature. While the feature is being developed, the code may be incomplete or temporarily broken. A branch allows you to save and commit your progress without affecting the main working version of the project.

In this assignment, you will replace the information in `student.txt` with your own information. You will create a branch to update the information without modifying the `main` branch.

First, view the branches in your repository:

```console
git branch
```

You should see the `main` branch:

```text
* main
```

The `*` indicates the branch that you are currently using.

Create a new branch named `update-info`:

```console
git branch update-info
```

View the branches again:

```console
git branch
```

You should now see both branches:

```text
* main
  update-info
```

Notice that you are still on the `main` branch. Creating a branch does not automatically switch to it.

Switch to the `update-info` branch:

```console
git checkout update-info
```

You can verify that you switched branches using:

```console
git branch
```

You should now see:

```text
  main
* update-info
```

Edit `student.txt` and replace the information with your own:

```text
Name: Your Name
GitHub username: YOUR_GITHUB_USERNAME
Email: YOUR_EMAIL
```

Since this repository is public, you may use your `noreply` email address for `YOUR_EMAIL` if you do not want to publish your personal email address.

Save the file and inspect the changes using the `diff` command:

```console
git diff
```

Stage and commit the changes:

```console
git add student.txt
git commit -m "update student information"
```

Push the new branch to GitHub:

```console
git push origin update-info:update-info
```

In this command, `origin` specifies the remote repository, while `update-info:update-info` specifies the branch mapping in the form `LOCAL_BRANCH:REMOTE_BRANCH`. Therefore, this command pushes your local `update-info` branch to a branch named `update-info` in your GitHub repository. Since the local and remote branch names are the same, this command could also be shortened to `git push origin update-info`.

You should now be able to see both `main` and `update-info` on GitHub.

## 11. Make a Different Change on `main`

Switch back to the `main` branch:

```console
git checkout main
```

You can verify that you are on `main` using:

```console
git branch
```

The `*` should now appear next to `main`.

Open `student.txt`. The file contains the original information because the changes that you made in the previous section exist on the branch `update-info`, and we are now on the branch `main`.

Edit `student.txt` to have the following information:

```text
Name: Morty Smith
GitHub username: mortysmithj22
Email: mortysmith@j22.example
```

Stage and commit them:

```console
git add student.txt
git commit -m "change student information to Morty Smith"
```

You have now changed the same lines of the same file differently on two branches.

## 12. Merge the Branches

Your changes on `update-info` are now complete, so you want to incorporate them into the main version of the project.

While on `main`, attempt to merge `update-info`:

```console
git merge update-info
```

Git should report a **merge conflict**.

A merge conflict occurs when Git cannot automatically determine how changes from two branches should be combined. In this case, both branches changed the same lines in `student.txt`, and Git does not know which change is correct.

Open `student.txt`. Git will mark the conflicting section using text similar to:

```text
<<<<<<< HEAD
Name: Morty Smith
GitHub username: mortysmithj22
Email: mortysmith@j22.example
=======
Name: Your Name
GitHub username: YOUR_GITHUB_USERNAME
Email: YOUR_EMAIL
>>>>>>> update-info
```

The section above `=======` contains the version from your current branch (`main`), while the section below it contains the conflicting version from `update-info`.

Resolve the conflict manually so that the file contains your own information. You must ensure that the conflict markers (`<<<<<<<`, `=======`, and `>>>>>>>`) have been completely removed.

Save the file.

## 13. Complete the Merge

Check the repository status:

```console
git status
```

Git still lists `student.txt` under **Unmerged paths** as `both modified`. Editing the
file does not tell Git that the conflict is resolved; you mark it as resolved by staging it.

Stage the resolved file:

```console
git add student.txt
```

Check the status again:

```console
git status
```
Git should now report that all conflicts are fixed but that you are still merging.

Complete the merge by creating a commit:

```console
git commit -m "resolve merge conflict"
```

Push the completed changes to GitHub:

```console
git push origin main
```

## 14. Inspect the Repository History

Git can display the branch and merge history graphically in the terminal (though this graph can be difficult to parse in larger projects). Run:

```console
git log --graph --oneline
```

Open your repository on GitHub in a browser and inspect the commit history.

## 15. Submission

Before submitting the assignment, verify that:

* Your GitHub repository contains `student.txt`.
* The version of `student.txt` on `main` contains your name, GitHub username, and email address.
* Your changes have been committed.
* Your commits have been pushed to GitHub.
* Your repository contains the `update-info` branch.
* Your repository history shows the branch and merge activity from this assignment.

Submit the URL of your GitHub repository through Moodle. 

> **Extra Credit:** You can receive up to 5 points of extra credit by submitting a pull request with a significant correction or improvement to this assignment. Minor errors, such as spelling or punctuation mistakes, may receive 1 point, while more significant corrections or improvements may receive additional credit.

## Issues and Pull Requests

GitHub also provides tools for discussing issues and proposing changes to a repository. We will use these tools for this assignment and throughout the course.

### Issues

If you encounter a problem with this assignment, create an **Issue** in the original repository:

https://github.com/ou-spinlab/ECE4510-Git-and-Github/issues

Before creating a new issue, check whether another student has already reported the same problem. If so, you can add additional information to the existing issue instead of creating a duplicate.

When creating an issue:

* Use a short, descriptive title.
* Clearly describe the issue and what you were trying to do.
* Include any relevant information (e.g., error messages, terminal output, etc...).
* If you are referring to a specific line or lines in a file, include a **permalink** to those lines rather than copying and pasting the contents. To create a permalink on GitHub:

  1. Open the file in the GitHub browser interface and view the file in **Code** view.
  2. Click a line number to select a single line. To select multiple lines, click the first line number and then hold `Shift` while clicking the last line number.
  3. Open the menu next to the selected line(s) and select **Copy permalink**.
  4. Paste the link into your issue.

  A permalink points to the specific version and lines of the file, making it easier for others to see exactly what you are referring to.

> **Important:** Do not include passwords, private SSH keys, access tokens, or any sensitive information in an issue.

### Pull Requests

If you identify an error in the assignment or repository, such as a typo, incorrect command, or unclear instruction, you are encouraged to correct it and submit a **Pull Request** to the original repository.

A pull request proposes that changes from your fork be incorporated into the original
repository.

At this point, your fork's `main` branch contains `student.txt` with your name and email
address. If you open a pull request from `main`, those commits are included in the proposed
changes. A pull request should contain only the change you are proposing, so create your
branch from the original repository rather than from `main`.

First, add the original repository as a second remote named `upstream`:

```
git remote add upstream git@github.com:ou-spinlab/ECE4510-Git-and-Github.git
```

You can confirm that both remotes are configured:

```
git remote -v
```

Download the current state of the original repository and create a branch from it:

```
git fetch upstream
git checkout -b fix-readme upstream/main
```

Your new branch now matches the original repository and does not contain `student.txt`.
Make your correction, then commit and push the branch to your fork:

```
git add README.md
git commit -m "briefly describe the correction"
git push -u origin fix-readme
```

Open your fork on GitHub. It should offer to open a pull request from `fix-readme`. Set the
base repository to `ou-spinlab/ECE4510-Git-and-Github` and the base branch to `main`.

Before submitting, open the **Files changed** tab and confirm that only the files you
intended to change are listed. If `student.txt` appears, your branch was created from the
wrong starting point.

In the pull request, you should briefly describe what you changed and why you changed it.

