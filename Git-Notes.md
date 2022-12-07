# Git notes

> These notes will cover the basics and some advanced concepts of git.
> These are one of the most frequetly used by me.

---

### Table of contents

- 1 [Pushing changes to the respository](#start)
  - 1.1 [Staging files](#staging)
  - 1.2 [Unstaging files](#unstaging)
  - 1.3 [Committing files](#committing)
  - 1.4 [Pushing files](#pushing)
  - 1.5 [Pushing a new local branch](#pushlocal)

---

<div id="start"></div>

### Pushing changes to the database

If you modified, added or deleted a file, version control wil tell you that the files have changed compared to the remote repository.
you can use `git status` to see which files changed compared to your repository. It will show you: modified, new (untracked) and deleted files.

<div id="staging"></div>

#### Staging files

If you want update those changes with the remote branch (Pushing) we first need to stage the changes. We can do that by using the following command: `git add .` which will add all the modified files to the commit state (ready to commit) but you can also use `git add [file name]` to stage specific files.

<div id="unstaging"></div>

#### Unstage Files

If you made a mistake while staging files you can unstage them by using `git restore --staged [filename]`
Notice were using a keyword called `--staged` which is flag for what type of restore you want to do in this case we want to undo the previous git command.
You can use other flags for example `--source` which will not only unstage your changes but will also go back to the last commited version.
meaning that the changes that you made to the file will be lost.
Lastly you can use the `--patch` flag which will allow you to restore individual chucks of a file you modifies.

<div id="committing"></div>

#### Committing files

Once we have stage the right files we want to push to the repository then its timr to commit them. We can do that byusing the following command: `git commit -m <message>`. The `-m` is needed to add a message to your commit. `<message>` is the place where you write the name of your commit. Make sure the commit message describes exactly what you changed so that other developers know what you changed without having to check the changed themselves. using the option `-a` will commit all changed files but will not include untracked files. (Untracked files are newly created files)
Using the `--amend` flag will will rewrite the very last commit you made and amend them with new changes.

> only use `--amend` on commits that aren't pushed yet.

<div id="pushing"></div>

#### Pushing files to the repository

Not that we have commited our changes its time to push them to the repository. We can push our commits to the repository with tis command: ~~`git push`~~ but this is bad practive as you're not specifiying which branch you want to push to and git will take the default branch which is the current working branch. unless you have a `tracking connection` set up with your branch. Its good practice to always specify which remote branch you want to push to like this `git push origin <branch>` this will now push your commit to the remote branch. `origin` refers to the remote branch here, and `<branch>` is the name of that remote branch.

To delete a remote branch we can use the flag `--delete` this will delete the remote branch. `git push --delete origin <branch>`

<div id="pushlocal"></div>

#### Pushing a new local branch

If youre pushing a newly created local branch to the remote repository its useful to add the `-u` option to keep track It makes sure that a tracking connection between the local and the newly created remote branch is established. Now its actually fine to use `git push` without specifying the remote branch as git now knows where to push its changes by looking at the tracking information.

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

After you resolved the conflicts you need to stage the new changes.
`git add .`

Then you need to continue the rebase:
`git rebase --continue`

Finally you want to force push your changes to your feature brwanch so they can be merged with main.
`git push --force origin feature-branch`

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
