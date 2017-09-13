<!-- permalink: 93c333da4f2f3512cf42e3a20574008c DO NOT DELETE OR EDIT THIS LINE -->
# README

This is just a collection of notes to myself about how to set up different things with programming and admin utilities

This collection of documentation is also serving as content for [demoing](markdowndemo.redeggproductions.com) my [markdown repository project](https://github.com/mredig/markdownrepo).

If you are reading this from the demo site, this is the GitHub [note source](https://github.com/mredig/Notes-to-Self). Also, this is Michael's [GitHub](https://github.com/mredig/) if you are interested in any other projects he maintains or contributes to.


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
