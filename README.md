This is just a collection of notes to myself about how to set up different things with programming and admin utilities

This collection of documentation is also serving as content for [demoing](markdowndemo.redeggproductions.com) my [markdown repository project](https://github.com/mredig/markdownrepo).


### load scripts
Note that the scripts aren't necessary - they directly relate to topics covered in these notes, but aren't necessary to the notes themselves.

How to get the submodules to load their repositories
* `git submodule init`
* `git submodule update --recursive`
* [reference](https://stackoverflow.com/questions/1535524/git-submodule-inside-of-a-submodule-nested-submodules)
* [updating the repositories](https://stackoverflow.com/questions/8191299/update-a-submodule-to-the-latest-commit)
	* looks like it's a matter of
		1. `git submodule update --remote --merge`
		1. `git add [submodule directory]`
		1. `git commit -m "updated submodules"`
