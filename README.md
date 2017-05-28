# Notes

This is just a collection of notes to myself about how to set up different things with programming and admin utilities - I suppose anyone may feel free to add any additions and ideas of their own with a pull request


### load scripts
Note that the scripts aren't necessary - they directly relate to topics covered in these notes, but aren't necessary to the notes themselves.

Right now, this section is no more than scratch notes:

One or some combination of these should get the scripts to load with all their dependencies

* `git submodule update --init --recursive`
* `git submodule update --recursive`
* `git clone --recursive`
* [reference](https://stackoverflow.com/questions/1535524/git-submodule-inside-of-a-submodule-nested-submodules)
* [updating the repositories](https://stackoverflow.com/questions/8191299/update-a-submodule-to-the-latest-commit)
	* looks like it's a matter of
		1. `git submodule update --remote --merge`
		1. `git commit -m "updated submodules"`
