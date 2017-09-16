<!-- permalink: 39724b3ed986620d8d166863e48bb5e8 DO NOT DELETE OR EDIT THIS LINE -->
# Forbid Access in Apache

For example, forbid access to *.git* directories

	<Directory  ~ "\.git">
		Order allow,deny
		Deny from all
	</Directory>

Or forbid access to files that start with *.git* (like *.gitignore*, *.gitmodules*, etc)

	<FilesMatch "^\.git">
		Require all denied
	</FilesMatch>
