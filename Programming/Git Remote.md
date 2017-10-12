# Create a Git Remote

#### server portion

1. connect to remote server:
                * `ssh user@server`
1. change directory
                * `cd /path/to/git/stuff`
1. create an empty folder for the new master repository
                * `mkdir newGitProject.git`
1. create an empty git repo:
                * `git init --bare`

#### local repo portion

1. from your git repo, run
                * `git remote add origin user@server:/path/to/git/stuff/newGitProject.git`
1. Push existing contents to the new server:
                * `git push origin master`
1. Henceforth, you should be able to run
                * `git push`
