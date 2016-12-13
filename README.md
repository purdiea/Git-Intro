# GitHub Intro
Contains useful commands for using GitHub.  See also [Tech Training](https://sites.google.com/a/moveon.org/moveon-wiki/tech/tech-trainings/introduction-to-git-version-control) reference
  
### Set up connection, navigate to folder, and clone repository

* Test whether the ssh is running/active (?)

 >eval "$(ssh-agent -s)"

 Returns something like Agent pid 1434 which I think means it's active.  

* Connect to the ssh we want

 >ssh-add ~/.ssh/github_id_rsa
 
 Enter your passphrase for GitHub (created when I created the file github_id_rsa and saved in 1Password). (I think in theory I shouldn't have to do this each time but for now it appears I have to do it.)

* Navigate to directory where you want to store GitHub repositories.
 >cd /Users/amywhite/Dropbox/MoveOn/GitHub

* Clone a git-hub repository.  

 Go to the repository you want to clone online and copy the address by selecting the green button _"Clone or Download"_ - then make sure Use SSH is selected, and copy the address.  (The https version is not compatable with 2 factor authentication in GitHub). In the terminal, run the following: 

 >git clone git@github.com:sandramchung/choc-chip.git
 
 You can also add an optional name at the end of this command if you want to name it something different from the repo version.

### Looking at repository, editing file, and pushing back to GitHub

* Investigate repo

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

 Open the .txt file and make some changes. You can do this by navigating to the text file on your hard drive, opening, editing, and saving it, or opening it using a command line text editor like nano or vim.  Nano has an on-screen cheat sheet of commands while vim has more power and options but is less user friendly. Or you can designate a program to open the file like R Studio if editing an R file or a text editor like TextWrangler.
 >nano recipe.txt 

 > or

 >vim recipe.txt

 > or 
 
 > open -a TextWrangler recipe.txt

 You can check the status of your changes by using git status.  You'll see that recipe.txt is in red and shown as modified.  
 >git status

* Send changes to GitHub

 You now need to add, commit, and upload (push) the changes for them to be saved on git hub. 
 
 Adding changes
 >git add recipe.txt
 
 >git status
 
 Now it shows as modified but the color is green

 Committing changes - you have to include some note
 >git commit -m "Don't share with friends"

 Pushing changes to online.  You specify the [repository] and [branch] in the git push command.  Since I didn't create a second branch of this repo, the branch is master.  I think the default repository name is origin but I'm not sure about that... 
 >git push origin master

 And now you've edited your first GitHub repo!
 
 You can also update your local copy by pulling the file over again.  This is important if someone else modified and pushed their version of the repo while you were working on your local copy.
 > git pull origin master


