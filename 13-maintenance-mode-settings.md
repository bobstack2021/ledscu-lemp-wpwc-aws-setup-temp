# BEST ARTCLE TO HAVE COME OUT TO DATE
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