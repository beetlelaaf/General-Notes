# Git notes

> These notes will cover the basics and some advanced concepts of git.
> These are one of the most frequetly used by me.

### Staging Modified Files
`Git add [file name]` 
Will stage modified files so the can be committed.

`Git add .` 
Adds all the modified files to the commit state (ready to commit)

### Unstaging files (Restore)
`Git restore —gitstaged [file name]`
Unstage staged files.

`Git restore [filename]` 
Restore file changes (unstaged changes)

### Commiting files
`Git commit  -m [message]` 
Commits the staged files to the commit state.Here you give it a message to indicate what you’re pushing to the repository.

### Pushing files to the repository
`Git push`
Pushes your commits to the repository on the current branch you’re in.

`Git push origin [branch name]` 
Pushes your commits to origin branch

### Pulling changes form a branch 
`Git pull [remote] [branch]`
Allows you to pull changes from a branch that is ahead of your branch.

`Git pull [remote] [branch] —rebase`
This way you can pull form the main branch and rebes at the same time.

### Changing branches
`Git checkout` 
Switch (existing) branch.

`Git checkout -b [branch name]` 
Switch to a newly created branch.

### Branch Utilities
`Git status`
Gives the current status of the working tree.

`Git log` 
Shows all the current action that have taken place in the current branch like commits and merging. It also shows where the HEAD and Origin is. This way you can see how many commits you’re behind/ahead of the origin.

`Git log —oneline`
Does the same as git log but shows every step on one line.

`Git remote` 
List all the remote connections you have to other repositories.  

`Git remote -v`
Does the same b included the URL to the repository.

### Using git rebase
`Git rebase -I HEAD~N` 
- -I is used to make it an interactive rebase.
- HEAD to start from the HEAD and work down from newest commit to oldest.
- ~N is the number of commits we want to rebase.
> If we want to rebase up to 2 commits the command will look something like this: 
> `Git rebase -I HEAD~2`


A menu with multiple function will pop up with on the top the commits that you made with the word pick in front of it. change `pick` to `reword` on the commit you want change the message of.
Then save and quit the editor. Once you’ve done that a new window will pop up in which you’re able to change the commit message.
After successfully rebasing your changes you have to push those changes to the repository, but to push this you have to force this as git wouldn’t normally allow you to push this to the repository. (Git normally doesnt want you to chnage your commit history) You can force a push with: 
`Git push —-force origin [branch name]` (this is assuming you want to push to origin.)

#### Keywords that you can use inside git rebase

The `Reword` command allows you to change the message of a commit.
The `Squash` command allows you to squash a commit into your previous commit.
The `Drop` command will drop a commit along with its changes.