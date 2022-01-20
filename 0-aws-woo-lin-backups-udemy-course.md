# WEBSITE FILE BACKUPS
# SIMPLY RUN THIS COMMAND, COPY/PASTE WITH REPLACING COMPANY NAME AND IF OU WANT READ ON AS A REFERENCE:
# VIDEO “66.)” AT 7:50 SHOWS HOW TO MAKE CRONTAB
# Will have the following crontab command scheduled but follow instructions
# because we need to make directors and chmod stuff:

# nano /etc/crontab
# 2 1     * * *   root    /bin/tar -zcf /root/site_backups/REDACTEDSITENAME-$(/bin/date +\%Y-\%m-\%d).tar.gz /home/REDACTEDSITENAME/
# 2 2     * * *   root   mysqldump --add-drop-table --databases REDACTEDSITENAME > /home/REDACTEDSITENAME/backups/db/$(/bin/date +\%Y-\%m-\%d).sql.bak

# Preface: throughout this document, we’ll be using the “$getFILL” variable name to illustrate which areas needed to be filled in… 
#
#
#
# New /etc/crontab
# Tarsnap - backing up onsite backups to onsite (AWS S3)
# 3,2,1 rule = 3 copies of your data
# 1 Backup within your production environment
# 2 Backup on the same server
# 3 Off-site backup by using something like tarsnap OR you could just copy it over to another system
# 
# Backing this up - EVERY DAY
# 
# We’re going back up the REDACTEDSITENAME home directory (because it contains the website)
# 
# Commands to check the contents of where you’re going to be backing up:

ls /home
ls /home/REDACTEDSITENAME/

# Commands to actually back up the website files:

mkdir /root/site_backups
tar -zcf /root/site_backups/REDACTEDSITENAME-$(/bin/date +\%Y-\%m-\%d).tar.gz /home/REDACTEDSITENAME/

# To check the results of the backup
# run:

cd /root/site_backups/
ls
ls -alh
du -sh /home/REDACTEDSITENAME

# This will show how much space we saved by compressing this in addition to archiving it. We can get this down to about a quarter of the original size by compressing AND archiving
# Now we’re going to use the system-wide “crontab” to schedule these automatically. First thing you want to do is copy the command we have in section “2.b.”
# run:

nano /etc/crontab

# We can do this in root as well but running:
# crontab -e
# BUT - we prefer to do this system-wide type of deal, so we’ll stick with “a.i”
# run:

nano /etc/crontab

# Now we’re going to back up the files every day of the month as root and we’ll comment out the first line to explain what it is, then space out the next in accordance with the SHELL=/bin/sh & PATH info in the crontab file.
# CONTINUED FROM “d.i.” run (but don’t use this exactly - see “h”):

nano /etc/crontab

# THIS IS HERE FOR ILLUSTRATION PURPOSES AND 1/2
# REDACTEDSITENAME daily backup 
# 2  1	*  *  *   	root	tar -zcf /root/site_backups/REDACTEDSITENAME$(/bin/date +\%Y-\%m-\%d).tar.gz


# THIS IS 2/2 - USE THIS ONE:
# One last comment, we actually might want to do “/bin/tar” so we have an absolute path JUST in case someone is able to SNEAK something past root.
#  REDACTEDSITENAME daily backup 
# run:

2  1	*  *  *   	root	/bin/tar -zcf /root/site_backups/REDACTEDSITENAME-$(/bin/date +\%Y-\%m-\%d).tar.gz

# GREAT! Go to VIDEO 65 7:28 to see restoring the site files (step 1 of 2)
# run:

ls

# This prints the backup file. COPY/PASTE the backup file’s name.
# 
# Run:

tar -zxf REDACTEDSITENAME

# The “REDACTEDSITENAME-2021-09-22.tar.gz” is just an example file name…
# run:

ls
ls home/REDACTEDSITENAME/
mv /home/REDACTEDSITENAME/public_html /home/REDACTEDSITENAME/public_htmlHACKED

# Now we’ll do a recursive copy over to the other and there’s a difference between “home/” and “/home/”

cp -r home/REDACTEDSITENAME/public_html /home/REDACTEDSITENAME/

# In our directory, there’s something called “home” which is why there’s no slash in the recursive copy of “home/REDACTEDSITENAME/public_html” and the “/home/REDACTEDSITENAME/” is our real home directory. We’re going to copy over the “home/REDACTEDSITENAME/public_html” directory over to the “/home/REDACTEDSITENAME/” ← which is where our old “public_html” directory is which we’ve now renamed with “HACKED”
# run

ls /home/REDACTEDSITENAME/

# This returns our old directory “public_htmlHACKED” AND our new directory “public_html”
# THAT’S IT! For the backups using tar - now we’re going ot talk about the Database Backups and Restores.


# DATABASE BACKUPS - GO TO VIDEO 66 AND SKIP TO 8:30 for step 2 of 2 in restoring

# Store our MySQL root password in “root/my.conf”
# We’re going protect this by “chmod 600” - which is read and writable by root but not read or writable or executable by anyone else.
# This allows us to login with the password as the “root” user
# We can use this to do passwordless backups with the “mysql dump” utility
# We’re going to run mysql dump, add “drop-table” so we can 

# Create the password file as a script in the root’s home directory, so let’s make sure that we’re there. Run:

pwd

# should return “root/”
# If we’re not there, then run:

cd ~/

# then we’ll officially be in the “Root” home directory

# Create the password script file. Run:

nano .my.cnf

# Then we need to input the following:
[client]
user=root
password=[REDACTEDMYSQLROOTPASS]

# Login to MySQL by running:

mysql -u root

# Really quick, hit [ctrl + d] to log out and change the permissions to the root password script. Then, run:

chmod 600 .my.cnf

# You can now check permissions with users in a list format by running:

ls -alh
# Returns files directories users and permissions. if there’s a “d” in the beginning then it’s a directory.
# We’re goin to have to create the target directory “backupsdb” then run the scirpts and schedule them.
# run:

ls /home/REDACTEDSITENAME/
mkdir -p /home/REDACTEDSITENAME/backups/db
ls /home/REDACTEDSITENAME/
ls /home/REDACTEDSITENAME/backups/

# Now we’re going to drop in the “mysqldump” command:
# run:

mysqldump --add-drop-table --databases REDACTEDSITENAME > /home/REDACTEDSITENAME/backups/db/$(/bin/date +\%Y-\%m-\%d).sql.bak

# for example:
# mysqldump --add-drop-table --databases REDACTEDSITENAME >  /home/REDACTEDSITENAME/backups/db/$(/bin/date +\%Y-\%m-\%d).sql.bak
# Now, let’s list the files and check to make sure that it worked:

ls /home/REDACTEDSITENAME/backups/db/

# WILL RETURN FILE NAME!
# DATABASE & SITE RESTORES
# run:

cd /home/REDACTEDSITENAME/backups/db/

# Changing directories to where the backups ares

ls

# List out backup names to copy/paste for the restor command. Now restoring by running:

mysql -u root REDACTEDSITENAME < REDACTEDDBBACKUPFLE

# DONE! Website is restored :)
# CREATE THE CRONTAB FOR THIS NOW!
# RUN:

nano /etc/crontab

# Scroll down and add the following (before the first Crontab command):
2 2   * * *   root   mysqldump --add-drop-table --databases REDACTEDSITENAME > /home/REDACTEDSITENAME/backups/db/$(/bin/date +\%Y-\%m-\%d).sql.bak


To backup go to video 65 & backup files @ 7:28 to see restoring the site files (step 1 of 2)

Then go to video 66. @ 
