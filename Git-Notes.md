# Git notes

> These notes will cover the basics and some advanced concepts of git.
> These are one of the most frequetly used by me.

### Staging Modified Files

`git add [file name]`
Will stage modified files so the can be committed.

`git add .`
Adds all the modified files to the commit state (ready to commit)

### Unstaging files (Restore)

`git restore —gitstaged [file name]`
Unstage staged files.

`git restore [filename]`
Restore file changes (unstaged changes)

### Commiting files

`git commit -m [message]`
Commits the staged files to the commit state.Here you give it a message to indicate what you’re pushing to the repository.

### Pushing files to the repository

`git push`
Pushes your commits to the repository on the current branch you’re in.

`git push origin [branch name]`
Pushes your commits to origin branch

### Pulling changes form a branch

`git pull [remote] [branch]`
Allows you to pull changes from a branch that is ahead of your branch.

`git pull [remote] [branch] —rebase`
This way you can pull form the main branch and rebase at the same time.

### Changing branches

`git checkout`
Switch (existing) branch.

`git checkout -b [branch name]`
Switch to a newly created branch.

### Branch Utilities

`git status`
Gives the current status of the working tree.

`git log`
Shows all the current action that have taken place in the current branch like commits and merging. It also shows where the HEAD and Origin is. This way you can see how many commits you’re behind/ahead of the origin.

`git log --oneline`
Does the same as git log but shows every step on one line.

`git log main..` or `git log main.. --oneline`
Shows the commits of the current working branch.

`git remote`
List all the remote connections you have to other repositories.

`git remote -v` Does the same b included the URL to the repository.

`git stash`
Allows you to save your changes at the index if you want to have a clean working tree but not commit your changes yet.
this comes in handy if you want preform a command that requires use to commit your changes first. Now you can stash them and you're working tree would be clean.

`git stash pop`
Allows you to get all your changes back from the stash so you can continue working on it.

### Using git rebase

#### Performing a regular rebase

A regular rebase can be preformed by first fetching from the main/master branch:
`git fetch origin main`

Then (if you haven't already) checkout to the branch you want to rebase from:
`git checkout feature-branch`

Once you're in your branch, preform the rebase. Make sure you're rebasing from the `origin/main` and not `origin main` because we want to rebase fom the remote branch and not the local branch.
`git rebase origin/main`

Lastly we want to force push the changes to our branch using the following command
`git push --force origin feature-branch`

##### Handling conflicts while rebasing

If you experience any conflics while rebasing from main you can fix them inside the editor if you're using vscode.
With conflicts you can either choose to keep the code thats already in main, or use the `incoming changes` the incoming changes are the changes you have made inside your branch.
Usually you want to use the changes that were already inside main as one of the other developers might have changed them for their code to work. But it really depends on he situation so make sure you discuss this with a other developers that work on the same project as you.

#### Changing commits with rebase

`git rebase -I HEAD~N`

- -I is used to make it an interactive rebase.
- HEAD to start from the HEAD and work down from newest commit to oldest.
- ~N is the number of commits we want to rebase.
  > If we want to rebase up to 2 commits the command will look something like this:
  > `git rebase -I HEAD~2`

A menu with multiple function will pop up with on the top the commits that you made with the word pick in front of it. change `pick` to `reword` on the commit you want change the message of.
Then save and quit the editor. Once you’ve done that a new window will pop up in which you’re able to change the commit message.
After successfully rebasing your changes you have to push those changes to the repository, but to push this you have to force this as git wouldn’t normally allow you to push this to the repository. (git normally doesnt want you to chnage your commit history) You can force a push with:
`git push --force origin [branch name]` (this is assuming you want to push to origin.)

#### Keywords that you can use inside git rebase

The `Reword` command allows you to change the message of a commit.
The `Squash` command allows you to squash a commit into your previous commit.
The `Drop` command will drop a commit along with its changes.
