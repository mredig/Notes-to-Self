# Miscellaneous Linux and Debian Stuff

* Reconfigure *postfix* (or any package apparently)
	* `dpkg-reconfigure postfix`

* Mail packages
	* `apt install bsd-mailx`

* rsync with permissions and stuff
	* `rsync -rvlpogdstHEAX /original /copy`
		* `d` Transfer directories
		* `g` Preserve group
		* `l` Copy symlinks as symlinks
		* `o` Preserve owner
		* `p` Preserve permissions
		* `r` Recurse into directories
		* `s` No space-splitting
		* `t` Preserve modification times
		* `v` Verbose
		* `A` Preserve ACLs
		* `H` Preserve hard links
		* `X` Preserve extended attributes

* convert to UTF-8 text
	* `iconv -f UNICODELITTLE -t UTF-8 infile > outfile`
