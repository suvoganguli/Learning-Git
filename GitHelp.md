Git Help
==========

## Setting Git Prompt

Source: https://classroom.udacity.com/courses/ud775/lessons/2980038599/concepts/33417185870923
- Download 4 files: (also available in this repo)
> git-prompt.sh   
> git-completion.bash   
> bash_profile_course   
> .bash_prompt  
- If you already have a file in your home directory named .bash_profile, copy the content from bash_profile_course and paste it at the bottom of .bash_profile. Otherwise, move bash_profile_course to your home directory and rename it to .bash_profile.          
        OR  
-  Add the following (from bash_profile_course) to .bashrc:  
if [ -f ~/.bash_gitprompt ]; then    
    . ~/.bash_gitprompt    
fi    

Great source: https://git-scm.com/book/en/v2

## Git global setup

git config --global user.name "Ganguli,Suvo"  
git config --global user.email "subhabrata.ganguli@honeywell.com"  

### Create a new repository

git clone https://mn10pdvm40.htc.honeywell.com/gitlab/E183308/Suvo-UGV-TrajGen.git  
cd Suvo-UGV-TrajGen  

touch README.md  
git add README.md  
git commit -m "add README"  
OR  
git commit - it opens a text editor  
git push -u origin master  

### Existing folder

cd existing_folder  
git init  
git remote add origin https://mn10pdvm40.htc.honeywell.com/gitlab/E183308/UGV-TrajGen.git  
git add .  
git commit -m "Initial commit"  
git push -u origin master  

### Existing Git repository

cd existing_repo  
git remote rename origin old-origin  
git remote add origin https://mn10pdvm40.htc.honeywell.com/gitlab/E183308/UGV-TrajGen.git  
git push -u origin --all  
git push -u origin --tags  

### Discarding changes in a commit (say previous commit)  
See: https://support.beanstalkapp.com/article/1004-how-do-i-undo-things-in-git#5    
git revert <commit_ID>    (needs further testing)

### Discarding changes to a single file in a previous commmit
git checkout filename  
See: https://www.norbauer.com/rails-consulting/notes/git-revert-reset-a-single-file  

### Deleting files in repo and not in local folder

git rm --cached filename  
git commit -m "Deleting repo file"  
git push -u origin master  

### Deleting committed files
git commit -m "Something terribly misguided"  
git reset HEAD~  
<< edit files as necessary >>  
git add ...  
git commit -c ORIG_HEAD  

OR  

- Change your current branch to point to the older commit instead. You could do that with git reset --hard f414f31. However, this is rewriting the history of your branch, so you should avoid it if you've shared this branch with anyone. Also, the commits you did after f414f31 will no longer be in the history of your master branch.

- Create a new commit that represents exactly the same state of the project as f414f31, but just adds that on to the history, so you don't lose any history. You can do that using the steps suggested in this answer - something like:

_Use the following_

git reset --hard f414f31  
git reset --soft HEAD@{1}  
git commit -m "Reverting to the state of the project at f414f31"  

## Removing commit message  
git reset --soft HEAD~1  
    OR  
git commit --amend   

------------------------------------------
Ref: https://stackoverflow.com/questions/927358/how-to-undo-the-most-recent-commits-in-git

Say you have this, where C is your HEAD and (F) is the state of your files.

   (F)
A-B-C
    ↑
  master

You want to nuke commit C and never see it again. You do this:

git reset --hard HEAD~1  [BE CAREFUL WITH THIS .. IT WILL DELETE THE FILES IN COMMIT C]

The result is:

 (F)
A-B
  ↑
master

Now B is the HEAD. Because you used --hard, your files are reset to their state at commit B.

Ah, but suppose commit C wasn't a disaster, but just a bit off. You want to undo the commit but keep your changes for a bit of editing before you do a better commit. Starting again from here, with C as your HEAD:

   (F)
A-B-C
    ↑
  master

You can do this, leaving off the --hard:

git reset HEAD~1

In this case the result is:

   (F)
A-B-C
  ↑
master

In both cases, HEAD is just a pointer to the latest commit. When you do a git reset HEAD~1, you tell Git to move the HEAD pointer back one commit. But (unless you use --hard) you leave your files as they were. So now git status shows the changes you had checked into C. You haven't lost a thing!

For the lightest touch, you can even undo your commit but leave your files and your index:

git reset --soft HEAD~1

This not only leaves your files alone, it even leaves your index alone. When you do git status, you'll see that the same files are in the index as before. In fact, right after this command, you could do git commit and you'd be redoing the same commit you just had.

One more thing: Suppose you destroy a commit as in the first example, but then discover you needed it after all? Tough luck, right?

Nope, there's still a way to get it back. Type git reflog and you'll see a list of (partial) commit shas that you've moved around in. Find the commit you destroyed, and do this:

git checkout -b someNewBranchName shaYouDestroyed

You've now resurrected that commit. Commits don't actually get destroyed in Git for some 90 days, so you can usually go back and rescue one you didn't mean to get rid of.
-------------------------------------------------------------

## Recovering a destroyed commit
git reflog\
git checkout -b someNewBranchName shaYouDestroyed

## Show history of commits
git config --global color.ui auto\
git log

## Checkout
git checkout commit_id

## diff between working area and staging area
git diff

## diff between stating area and repot
git diff --staged

## diff between two commits
git diff commit_id1 commit_id2

## discard changes between working directory and status area
git reset --hard

## detatched head
If you are following along, you should run git checkout master before you commit. This is because your HEAD is still 'detached' from Lesson 1 when you checked out an old commit, and running this command will fix that. You'll learn more about what this command does later this lesson.

## checking out a different branch and compare with master
git log --graph --online master branch

## make new branch from experimental feature
git commit -b new_branch_name

## merging branches
git checkout master  
git merge master branch_name  
OR SIMPLY  
git merge branch_name (since master is checked out)  

## diff without knowing what the parent was after a merge
git show commit_id

## deleting branch
git branch -d branch_name

## abort merge
git merge --abort

## Merging branches
Example: https://backlog.com/git-tutorial/en/stepup/stepup2_1.html

## git diagram
git log --graph

## view last commit
git log -n1

## Save login/password
git config credential.helper store

## Resolve SSL Certificate problem: unable to get local issuer 
git config --global http.sslVerify false

## Removing remote
git remote -v  
> origin ...  
> temp ...  
git remote rm temp  

## Renaming remote
git remote rename oldname newname

## Deleting remote and local branch
$ git push --delete <remote_name> <branch_name>  ... remote  
$ git branch -d <branch_name>  ... local  (note, you may need to use --delete of force with -D)

## Cloning all branch
git clone https://github.com/suvoganguli/GIG-MPC.git  
git branch -a
git checkout -b expts origin/expts  
git branch  

## Workflow
git checkout master  
git merge master branch_name  
git push --delete <remote_name> <branch_name>  
git branch -d <branch_name>  

--------------------------------------------------------
## Reverting Working Copy to Most Recent Commit
To revert to a previous commit, ignoring any changes:  
git reset --hard HEAD  
where HEAD is the last commit in your current branch  
_________________________________________________________  
## Reverting The Working Copy to an Older Commit (THIS NEEDS TO BE TESTED)
To revert to a commit that's older than the most recent commit:

### Resets index to former commit; replace '56e05fced' with your commit code
git reset 56e05fced 

### Moves pointer back to previous HEAD
git reset --soft HEAD@{1}

git commit -m "Revert to 56e05fced"

### Updates working copy to reflect the new commit 
git reset --hard HEAD 
_________________________________________________________  

## Merge Abort

git merge --abort  

## Discard unchaged changes in Git

To unstage one file :  
$ git checkout _path-to-file_

Remember to replace _path-to-file_ with the actual file name.  

To unstage all files:  
$ git checkout -- .  

_________________________________________________________  

## Difference Between Commits

cherry-picking can give you the delta of a single commit rebased on top of another. That is:

$ git checkout 012345  
$ git cherry-pick -n abcdef  
$ git diff --cached  

This takes commit 'abcdef', compares it to its immediate ancestor, then applies that difference on top of '012345'. This new difference is then shown - the only change is the context comes from '012345' rather than 'abcdef's immediate ancestor. Of course, you may get conflicts and etc, so it's not a very useful process in most cases.  

If you're just interested in abcdef itself, you can do:  

$ git log -u -1 abcdef  
This compares abcdef to its immediate ancestor, alone, and is usually what you want.

And of course

$ git diff 012345..abcdef  
gives you all differences between those two commits.  

__________________________________________________________________  

### Start a new repo from terminal

git init  

git add .  (Adds the files in the local repository and stages them for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.)  

git commit -m "First commit" (# Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.)  

git remote add origin remote repository URL  (Sets the new remote)  
git remote -v  (Verifies the new remote URL)

git push origin master (Pushes the changes in your local repository up to the remote repository you specified as the origin)  



