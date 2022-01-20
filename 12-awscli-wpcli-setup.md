# INSTALLING THE AWS-CLI & WP-CLI

# SOURCES:
# WP-CLI: https://make.wordpress.org/cli/handbook/guides/installing/
# AWS-CLI https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
# If you’re running an X86 64 bit server, then use those instructions. If you’re using the ARM server, then use those instructions. The CLI is NOT based on the OS - it’s based on the Server.
# If on Ubuntu, make sure that “Unzip” is installed
# Navigate to /root/aws/dist/awscli/data/ec2/2016-11-15
# For JSON Architecture

# AWS-CLI Linux - Ubuntu T4G-EC2 Installation
#
# Step One (1): Simply copy/paste the following:
curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip"
apt install unzip
unzip awscliv2.zip
sudo ./aws/install
# Step Two (2): Then to check, just run:
aws --version
# OR - you can run: 
/usr/local/bin/aws --version

# WP-CLI Install
# The recommended way to install WP-CLI is by downloading the Phar build (archives similar to Java JAR files, see this article for more detail), marking it executable, and placing it on your PATH.
# WP-CLI Install Notes
# Step One (1): DOWNLOAD  wp-cli.phar using wget or curl. RUN:
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
# Step Two (2): Check that it works. RUN:
php wp-cli.phar --info
# Step Three (3) - OPTIONAL - To be able to type just wp, instead of php wp-cli.phar, you need to make the file executable and move it to somewhere in your PATH. RUN:
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
wp --info


# VERSION TWO (2)!!!
# # BEST ARTCLE TO HAVE COME OUT TO DATE
# URL: https://websitesetup.org/wordpress-into-maintenance-mode/#code
# Step 3: Add Maintenance Mode Code to functions.php
# With functions.php open in the editor, copy all of the code inside the file and save a copy of it to your desktop.
# Then, scroll to the bottom of the file and add the following snippet:

function wp_maintenance_mode() {
if (!current_user_can('edit_themes') || !is_user_logged_in()) {
wp_die('<h1>Under Maintenance</h1><br />Website under planned maintenance. Please check back later.');
}
}
add_action('get_header', 'wp_maintenance_mode');

# This is the default WordPress maintenance mode setting and message.
# If you want to edit what it says, replace this bit with your own wording:

<h1>Under Maintenance</h1><br/>Website under planned maintenance. Please check back later.

# When you’re happy with what it says, click “Update File”.