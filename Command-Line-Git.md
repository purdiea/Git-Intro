# GitHub Intro
Contains useful commands for using GitHub.  See also [Tech Training](https://sites.google.com/a/moveon.org/moveon-wiki/tech/tech-trainings/introduction-to-git-version-control) reference or https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/ and https://help.github.com/articles/connecting-to-github-with-ssh/ for more about connecting to GitHub via SSH (particularly if you get permission errors when trying to clone a repository.) 
  
### Set up connection, navigate to folder, and clone repository

#### All commands are run in the terminal 

(Do not log onto ssh moanalytics - just do from your machine)

* Test whether the ssh is running/active (?)

 >eval "$(ssh-agent -s)"

 Returns something like Agent pid 1434 which I think means it's active.  

* Check which ssh keys exist

> ls -al ~/.ssh

* Connect to the ssh we want

 >ssh-add ~/.ssh/github2_id_rsa 
 (This is the one on my personal computer, one on Analytics box is id_rsa)
 
 Enter your passphrase for GitHub (created when I created the file github_id_rsa and saved in 1Password). (I think in theory I shouldn't have to do this each time but for now it appears I have to do it.)

 If you need to check what SSH keys exist on your repo, visit https://github.com/settings/keys
 To create a new key, follow instructions here:  https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/
 If you do this from the analytics box, it will create a new key that everyone will need to use.  If you do it from your local machine then that is what you will use to connect to github from your local machine.
 
* Navigate to directory where you want to store GitHub repositories.
 >cd /Users/amywhite/Dropbox/MoveOn/GitHub

* Clone a git-hub repository.  

 Go to the repository you want to clone online and copy the address by selecting the green button _"Clone or Download"_ - then make sure Use SSH is selected, and copy the address.  (The https version is not compatable with 2 factor authentication in GitHub). In the terminal, run the following: 

 >git clone git@github.com:sandramchung/choc-chip.git
 
 You can also add an optional name at the end of this command if you want to name it something different from the repo version.

### Looking at repository, editing file, and pushing back to GitHub

* Investigate repo

 Checking how you are connected to GitHub
 >git remote -v

 If this is https: then you won't be able to access using 2 factor authentication.  Instead, you need to be connected via ssh  which will look like this `git@github.com:MoveOnOrg/analytics.git`

 If you are in the https version and what to change, you can run this
 >git remote set-url origin git@github.com:MoveOnOrg/analytics.git

 The last part `analytics` is the name of the repo.

 Look at files within the directory, then open up the repository that you cloned and look in it.
 >ls
 
 >cd choc-chip

 >ls

 You can see the README.md and the actual text file that the repo contains.  It could contain R programs, python code, really anything you want.  
 
 Check the log of commits for the file
 >git log

 See what the differences are between prior commits and the current version.  (The log alpha numeric code is the commit #
 >git diff ee3945b6213756dccffd98259f4b027d8534046b
 
 Check which repo you are currently connected to
 >git remote -v
 
 Remove the specified (origin) repo
 >git remote remove origin
 

* Edit the .txt file

 Open the .txt file and make some changes. You can do this by navigating to the text file on your hard drive, opening, editing, and saving it, or opening it using a command line text editor like nano or vim.  Nano has an on-screen cheat sheet of commands while vim has more power and options but is less user friendly. Or you can designate a program to open the file like R Studio if editing an R file or a text editor like TextWrangler.  The YouTube GitHub for Noobs likes Atom
 >nano recipe.txt 

 > or

 >vim recipe.txt

 > or 
 
 > open -a TextWrangler recipe.txt
 
 > or
 
 > atom .
 Opens current repo and you can select which file to edit
 
 You can check the status of your changes by using git status.  You'll see that recipe.txt is in red and shown as modified.  
 >git status

* Send changes to GitHub

 You now need to add, commit, and upload (push) the changes for them to be saved on git hub. 
 
 Adding changes
 >git add recipe.txt 
 
 OR
 
 >git add -u 
 
 Adds all changes for all files excluding untracked files.  If you have a brand new file that hasn't been loaded to github at all, it won't show up in the red list above but instead will show up in the untracked list below.  To add it to the tracked list, you have to explicitely do git add filename.   
 
 >git status
 
 Now it shows as modified but the color is green

 Before committing any changes, you should pull the directory again.  This will update your local copy by pulling the file over again.  This is important if someone else modified and pushed their version of the repo while you were working on your local copy.
 > git pull origin master

 Committing changes - you have to include some note
 >git commit -m "Don't share with friends"

 You can also add and commit in one step
 > git commit -am "Don't share with friends"
 
 Pushing changes to online.  You specify the [repository] and [branch] in the git push command.  Since I didn't create a second branch of this repo, the branch is master.  I think the default repository name is origin but I'm not sure about that... 
 >git push origin master

 And now you've edited your first GitHub repo!
 
### Comparing local version to GitHub

`git pull` actually does two things - it fetches the data from git hub and merges with the local version.  If you think there may be conflicts and do not want to write over your local changes when pulling from the master, you can just fetch and then compare the files.
>git fetch origin master

Then look at the summary of differences across files
>git diff HEAD..origin/master

If you want to merge the master to whatever branch you have open locally, do 
>git merge origin/master


### Fixing conflicts

If you try to merge your changes to the master, you may get a conflicts warning if there have been changes made to the master that are not reflected in your local directory.  if that happens, open the file with conflicts and look for the `======` record.  The data above this line is what you have locally and the data below is what is contained in the master.  Delete the information you don't want as well as the line with `====` and the lines with `<<<<` and then save the file and re-merge.

`dd` deletes a line when using VIM

### Branching repository

 Check which branch you are currently in.  Master is the "trunk"
 >git branch

 Create a new branch called pie
 >git branch pie

 Now checkout this branch.  Which ever branch you have checked out is the branch which will be affected by any edits you make.
 > git checkout pie

 Alternatively, you can create and checkout a branch in one step.  We'll create a new branch called brownie.
 > git checkout -b brownie

 Make sure you are in the brownie branch
 >git branch

 To see the relationship of the trunk and branches you can graph the tree
 >git log --graph

 Now make changes to file in the brownie branch and add and commit
 > vim recipe.txt
 
 > git commit -am "added brownie instructions"
 
 Now merge to master. 
 
 
 ### Untracked Files
 
  We do not want to load files that contain credential information to the github repository.  To have github ignore these files, we need to add them to the .gitignore list. 
  
  >cd ~
  
  >vim .gitignore
  
  Add the path and file name that you want to ignore and save file.
  
  ### Removing sensitive files from GitHub
  
  If a file with authentication data was merged to GitHub, you cannot simply delete the file because its history will still remain.  Instead, you need to follow the complicated process of git-filter-branch described here.
  https://help.github.com/articles/removing-sensitive-data-from-a-repository/

 Step 1 pull most recent version from github: 
 > pull origin master

 Step 2 make copy of settings file with new name: 
 Navigate to desired directory
 > cd scripts/fundraising/monthlymodel
 > cp file.ext new_file.ext

 Step 3 add settings file and copied file name to .gitignore: 
 > vim .gitignore
 file.ext
 new_file.ext

 Step 4 push changes to .gitignore to repo: 
 > git add 
 > git commit -m “updating .gitignore”
 > git push origin master

 Step 5 remove settings file and all history from github 
 Navigate to home directory
 > cd ~
 > git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch scripts/fundraising/monthlymodel/file.ext' --prune-empty --tag-name-filter cat -- --all

 Step 6 push changes: 
 > git push origin --force --all

 Step 7 move copy of settings back to original file name
 Navigate back to directory
 > cd scripts/fundraising/monthlymodel
 > mv new_file.ext file.ext

 Step 8 verify file no longer exists on Github.com and check git status that local and master are up to date
 > git status

