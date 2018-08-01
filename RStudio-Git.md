# Using Git with RStudio

To use GitHub with RStudio, first create your repo on GitHub.  Then in RStudio, do File -> New Project -> Version Control -> GitHub, and enter the HTTPS link to your repo and navigate to the directory where you want to clone the repo on your machine.
 
To save changes to GitHub.com, first save the R file you are working on into the Git repository folder that you cloned.  (It will automatically be saved there if it's part of the Rproj file.)

Once you have saved the file, check the staged box next to the file in the top right of RStudio under the Git tab.  Select Commit, add your message, and in commit.  Then to push the changes to GitHub, use the upward green arrow under the Git tab in RStudio.  You will be prompted for your GitHub username and then password.  Your normal password for logging into GitHub.com *will not work* if you have 2FA on your account.  Instead, you will need to get a Personal Access Token and use that instead.  (See here for details https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/GitHub.) 

Alternatively, you can use Git Desktop to manage your commits and pushing to the master.  Go to the associated repository, click the Changes tab, enter a summary and description of what you've done for changes, then say Commit to Master.  Then you still need to push your changes by selecting Push origin in the upper right.  And that's it!

Or, you could even use the command line in RStudio to commit your changes and push to the master. 

Any files you don't want loaded to GitHub cloud should be listed in the .gitignore file, like config.R type files.

This website is a great resource for using GitHub with RStudio. http://happygitwithr.com/rstudio-git-github.html
