# Input this code at the end of the "material-design-google" theme's "functions.php"
# File to put the website into "Maintenance Mode" 
# Remove this code to make integrations
# In between a rock and a hard place with this one. It's nto best practice and I believe this specific code actually copy/pasted incorrectly.
# Can use wp-cli by running:
wp maintenance-mode activate
# And htis should be sufficient. When you make changes, WP automatically removes maintenance mode so then you have to log back into AWS and blah blah - at any rate, this will be edited in the bottom of the themes directory if one does NOT use the wp-cli. The only caviate is that it needs to be removed before upates are run otherwise it could crash the whole site.
# Go to thebottom of your themes functions.php file and copy/paste the following:

function wp_maintenance_mode() {
if (!current_user_can('edit_themes') || !is_user_logged_in()) {
wp_die('<h1>Under Maintenance</h1><br />Website under planned maintenance. Please check back later.');
}
}
add_action('get_header', 'wp_maintenance_mode');