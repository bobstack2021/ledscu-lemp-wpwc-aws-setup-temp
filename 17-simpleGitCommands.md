# This will serve as a very BASIC introduction to the 'Git' commands

# To initialize a repository, run:

git init

# To add a file from the local repository (dev0-1) to the staging area (stg-0-1), run:
git add <file-name>

# To check which files are in the staging area or have changed and need to be staged, run:
git status <file-name>

# To remove a file from the staging area, run:
git rm --cached <file-name>

# To add all files with a specific file ending, such as '.md', to the staging area, run:
git add *.md

# To remove all files with a specific file ending, such as '.md' from the staging area, run:
git rm --cached *.md

# To add ALL FILES to the staging area (except those in the .gitignore file), run:
git add .

# To create the '.gitignore' file, which allows you to list files within the repo that should NOT be added when committing to GitHub, run:
touch .gitignore

# To add files to the '.gitignore' file, run:
nano .gitignore
# list the file, then hit ctrl + o (as in hold control, press o and release) to write, then ctrl + x (as in hold down control, hit x and then release) to exit the file editing mode.

# To Commit files to the GitLab, BitBucket, GitHub etc. version control cloud system(s), run:
git commit
# Once you run 'git commit' -> you'll be in the 'vim editor' and will need to press the letter "i" to go into editor mode and be able to write.
# To get OUT OF VIM EDITOR MODE - HIT ESCAPE then ':wq' and hit enter
# For the initial commit, simply uncomment 'initial commit' by deleted the hashtag, then :wq to exit.
# This actually seems to either be different within Visutal Studio Code (I use VSCodium for Linux), and one can just simply operate with normal commands such as ctrl+o, ctrl+x. 
# TO SKIP THE EDITING STAGE: let's say that you committed, then edited again, all you have to do is run:
git commit -m 'this is where you'd add a quick note about the change in single quotes'
# Then it'll have skipped over the editing portion.
#
#
# BRANCHES - way to work on the code without affecting the master. To CREATE A BRANCH, RUN:
git branch login
# This will create another branch called 'login'
# If you're not in this branch and you want to enter the 'login' branch, run:
git checkout login
# Then it'll take you to the login branch. You can make your changes and commit them by running:
git add -m 'another change'
# Then switch back to the "master" branch by running:
git checkout master

# The login branch files will disappear BUT they did - indeed - change. You can 'MERGE' these if you'd like down the road and this is how multiple developers work together. While in the master, run:
git merge login
# Then the editor will open back up. Press 'i' to enter editor mode, add the reason for the merge (i.e. 'added login'), then hit:
:wq 
# hit enter and BOOM! Merged.