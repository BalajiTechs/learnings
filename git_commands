#create local git repo
git init

#add a file 
git add <file>

#add all modified folders
git add .

#get info about current git repo
git config -l

-----------------------------------------------------------------
#Flow for commiting changes

1. first clone the repo on local
 $ git clone <git repo url> <folder where to clone>
2. Do some changes
3. Add the changed file to staged area
 $ git add <filename>
4. Commit the changes locally
 $ git commit -m "your messege"
5. Push the changes to the git repo
 $ git push

-----------------------------------------------------------------
#Change the git url
git remote set-url origin https://github.com/BalajiTechs/linux-learnings

#List all remotes
git remote -v

==============================================================================
List files changed in a commit
git diff-tree --no-commit-id --name-only -r

==============================================================================
get authors details of changes between 2 commits
git log --pretty=format:"%an" prevTestCommit..lastTestCommit | sort | uniq
git log --pretty=format:"%ae" prevTestCommit..lastTestCommit | sort | uniq

==============================================================================
Tweaking checkout behaviour
$ git config --global core.filemode false //TODO
$ git config --global core.longpaths true //allow long paths
$ git config --global core.autocrlf false //use when working on windows as well as linux
$ time git clone <clone url> //clone and print timings