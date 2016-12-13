# Git-Intro
Contains useful commands for using GitHub

single return
# pound
- single dash
-- double dash
// double backslash
  tab 
  
- Test whether the ssh is running/active (?)
  eval "$(ssh-agent -s)"
Returns something like Agent pid 1434 which I think means it's active.  

- Then tell it to connect to the ssh we want
ssh-add ~/.ssh/github_id_rsa
- Then enter your passphrase for GitHub (saved in 1Password).  I think in theory I shouldn't have to do this each time but for now I appear to have to do it.


- Navigate to directory where you want to store GitHub repositories.
cd
/Users/amywhite/Dropbox/MoveOn/GitHub

- Clone a git-hub repository.  Go to the repository you want to clone and copy the address by selecting the green button Clone or Download - then make sure Use SSH is selected, and copy the address.  In the terminal, run the following: 
git clone git@github.com:sandramchung/choc-chip.git
- Actually I could get this to work but not the SSH one: https://github.com/sandramchung/choc-chip.git

- Look at files within the directory, then open up the repository that you cloned
ls
cd choc-chip
ls

- You can see the README.md and the actual text file that the repo contains.  It could contain R programs, python code, really anything you want.  Open the .txt file and make some changes.  You can do this by navigating to the text file on your hard drive, opening, editing, and saving it, or opening it using a command line text editor like nano or vim.  Nano has an on-screen cheet sheet of commands while vim has more power and options but is less user friendly. Or you can designate a program to open the file like R Studio if editing an R file or a text editor like TextWrangler.
nano recipe.txt 
- or
vim recipe.txt
- or 
open -a TextWrangler recipe.txt

- You can check the status of your changes by using git status.  You'll see that recipe.txt is in red and shown as modified.  You now need to add, commit, and upload (push) the changes for them to be saved on git hub. 
git status

- Adding changes
git add recipe.txt
git status
- Now it shows as modified but the color is green

- Committing changes - you have to include some note
git commit -m "Don't share with friends"

- Pushing changes to online.  You specify in git push the [repository] and [branch].  Since I didn't create a second branch of this repo, the branch is master.  I think the default repository name is origin but I'm not sure about that... 
git push origin master


- Other handy commands: 
- See what repos you are connected to
git remote -v

- Remove the specified (origin) repo
git remote remove origin

- Add specified repo
git remote add origin git@github.com:sandramchung/choc-chip.git


