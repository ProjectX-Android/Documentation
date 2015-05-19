# Gerrit

[Gerrithub](https://review.gerrithub.io/#/admin/projects/?filter=ProjectX) is our platform to review code before merging it into our Git repos. Everyone can push commits there. You just need to set it up:

## Setup

You can push to gerrit via Windows or Linux. The clients just need to be set up a little bit different.

Windows: Use Git PowerShell, [Download](https://windows.github.com/)
**Lines marked with # are for Linux users only**
**Lines marked with * are for Windows users only**

	cd ~/.ssh
	ssh-keygen -t rsa -C "your-email@domain.com"
* go to gerrithub settings → ssh public keys
* click on add key
* copy the content of ~/.shh/id_rsa.pub to the box in gerrit settings

		(#)sudo apt-get install python-pip
		(#)sudo pip install git-review
		(#)git config --global review.review.gerrithub.io.username "gerrit username"
		(#)git config --global review.review.gerrithub.io.email "email you registered with"

##Cloning

	git clone ssh://USERNAME@review.gerrithub.io:29418/ProjectX-Android/REPONAME && scp -p -P 29418 USERNAME@review.gerrithub.io:hooks/commit-msg REPONAME/.git/hooks/

## **IMPORTANT**

* **Always, no matter if you are pushing or updating, make sure that you dont have any staging changes (commit which are on gerrit but not on Git) on your local repo. Always “git reset --hard COMMITID(of the latest commit on GITHUB)” before making changes!**

* **If you edit a file on Linux, it automaticly generates a backup file which is called the same but with an ~ at the end. Make sure you delete it before the git add command!**

## Uploading a change

	#ssh-add (only if you get errors while pushing)
	cd REPONAME
* make your changes

		git add -A  //to add all changed files to your next commit
		git commit -s

### Linux:
* (#)a nano will pop up where you can enter the commit message, first line is the title, the rest will be the change description

		(#)cntr+o
		(#)cntr+x

### Windows:
* *a text editor will pop up where you can enter the commit message, first line is the title, the rest will be the change description
* *save the file
* *close the text editor

* push the change

		git push origin HEAD:refs/for/BRANCHNAME

## Uploading a Patchset

If you want to change something in your already uploaded commit, but dont want to upload a new one, you can upload a Patchset

* your local repo must be at the commit you want to patch (if it isnt, git reset --hard you cherry pick the commit from gerrit)
* change the files you want

		git add -A
		git commit --amend
		git push origin HEAD:refs/for/BRANCHNAME

## Other useful commands

* to squash all unmerged commits into one

		git rebase -i 

* to change the author of the latest commit in order to keep correct authorship

		git commit --amend --author="Author Name <email@address.com>" 

* adds a specific branch of a project as a remote which you can fetch 

		git remote add --track BRANCH REMOTENAME LINK_TO_REPO 

* to compare your local copy with the remote repo

		git diff REMOTE/BRANCH
