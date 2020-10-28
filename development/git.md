# Help
List all the commands or get information on a specific command:
```
$ git help [command-name]
```

# Configurations
_List current configurations:_
```
$ git config --list
```
The local configuration will override the global ones.

There are three levels of configuration in git:
- local → for a single repo (`--local`). They are  stored in *.git/config*.
- global → for your user (`--global`). They are stored in *~/.gitconfig*.
- system → for all users in the machine (`--system`).

_Check the value of a specific configuration:_
```
$ git config [option] user.<key>
```

## Initial Configs
You need to configure your username and email for record keeping purposes.
```
$ git config --global user.name "My Username"
$ git config --global user.email "myemail@email.com"
```

_Get colors on the output of the command line:_ <small>(default since git v1.8.4)</small>
```
$ git config --global color.ui true
```

_Specify which editor to use for interactive commands:_
```
$ git config --global core.editor <editor>
```

_Specify the merge tool to use:_
```
$ git config --global merge.too <tool>
```

_Set the default of push behaviour to just push the current branch:_ <small>(default since git v2.0)</small>
```
$ git config --global push.default simple
```

_Set the default of pull behaviour to rebase instead of merging:_
```
$ git config --global pull.rebase true
```

_Enable Reuse Recorded Resolution (ReReRe):_
```
$ git config --global rerere.enabled true
```
It will record all fixes to merge conflicts, and reuse them automatically if the same conflict recurs. Particularly useful when cherry picking to multiple branches or constantly rebasing.

### Auto-correcting line breaks formats
On Unix-like systems (changes CR/LF to LF on commit – fixes any Windowns line endings that get introduced).
```
$ git config --global core.autocrlf input
```
	
On Windows systems (changes LF to CR/LF on checkout – converts back to LF on commit).
```
$ git config --global core.autocrlf true
```
	
On Windows-only projects (does no conversion – everyone expects CR/LF).
```
$ git config core.autocrlf false
```

If somebody forgets to set their config: create *.gitattributes* in the root of the project and set the conversion settings.
```
*       text=auto

*.html  text
*.css   text

*.bat   text eol=crlf
*.sh    text eol=lf

*.jpg   binary
*.png   binary
```
- `text=auto` → choose conversion automatically.
- `text` → treat files as text - convert to OS's line endings on checkout, back to LF on commit.
- `text eol=crlf` → convert to specified format on checkout, back to LF on commit.
- `binary` → treat files as binary - do no conversion.

## Ignoring files
File that includes all the files and directories we don't want to include in our repository. Create a file called *.gitignore* and inside write paths of what you don't want.\
One file you may not want to add are logs files.

If the exclusion is only local, *e.g.* you don't want to share a file/folder with your colleges, add a line to *.git/info/exclude*.

## Aliases
_Create new alias:_
```
$ git config --global alias.<name> <commands>
```

_Create lol alias (log output format):_
```
$ git config --global alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"
```

_Run the command:_
```
$ git myalias
```

It may be useful to set alises for commands you use often, such as status (`st`), checkout (`co`), brach (`br`), and commit (`ci`).
Some aliases recommended are:
- `git s` → `git status -s`
- `git lg` → `git log --oneline --decorate --all --graph`

# Basics
Initialize project, setting up the Git control structures. In this directory will be the local project files and the history snapshots of your code.
```
$ git init <project-name>
```

_Check what's in the staging area:_
```
$ git status
```
- `-s` → silent mode.

It will show what has changed since the last commit on the working branch.

_Put files into the staging area, ready to permanently be commited:_
```
$ git add <file-name>
```
-	`--all` → adds all new or modified files.
-	`-u` → stages modified and deleted files.

`"*.txt"` will add all txt files in the whole project, whereas without the `"` it will only add the txt files in currrent directory.

_Remove file from repository:_
```
$ git rm <file-name>
```
-	`--cached` → stop tracking the file for changes.

_Create a snapshot of the staging area and add a commit to the top of the timeline:_
```
$ git commit -m "<commit-message>"
```
-	`-a` → add changes from all tracked files. Doesn't add new (untracked) files.
-	`-m` → commit message.
-	`--amend` → changes the last commit, adding any staged files to it. You can also specify a new commit message using `-m` option.

Commit messages are very important. You want to be as descriptive as possible as to what they do. Use the present tense, not the past.

## Reseting modifications
Unstage file:
```
$ git reset HEAD <file-name>
```
`HEAD` refers to the last commit on the current branch.

_Reset modifications to the state the specified file was in at the last commit:_
```
$ git checkout -- <file-name>
```

_Undo last commit:_
```
$ git reset [options] [HEAD^]
```
-	`--soft` → put changes into staging.
-	`--hard` → undo last commit and all changes.

`HEAD^` means the commit one before current `HEAD`. If `HEAD` is not specified, it will undo the uncommitted changes.

_Undo a given commit, but create a new one without deleting the older one:_
```
$ git revert <commit-hash>
```
It won't touch the commit history - you can still see all of the commits in your history, even the reverted ones.\
You will be thrown to a editor to write a commit message.

## Restoring commits after a hard reset
Git never deletes a commit. Git keeps a second log, only in your local repo, called **reflog**. It's updated anytime `HEAD` moves (due to new commits, checking out branches, or resetting). If you clone a repository, reflog will reset.
```
$ git reflog
```

_Show reflog info in full log format:_
```
$ git log --walk-reflogs
```
It will include reflog shortnames and messages

_Restore a commit:_
```
$ git reset --hard <commit>
```
You can use the reflog shortnames.

_Restore a branch:_
```
$ git branch <name-branch> <commit>
```

# Remote Repositories
Create a repository in a service (*e.g.* Github). They will give you the repository link to upload the changes.

_List remove repositories:_
```
$ git remote -v
```

_Add a new remote repository:_
```
$ git remote add <name-for-repository> <repository-url>
```
`origin` is usually the name used for the main repository.

_Remove a remote repository:_
```
$ git remote rm <name-repository>
```

_Push your application in master to the repository:_
```
$ git push -u <repository-name> <branch-name>
```
-	`-u` → makes it so next time you push you don't have to specify the name of the branch.
-	`-f` → force push.
You will need to login to Github.

_Update your local files from a remote repository:_
```
$ git pull
```
-	`--rebase` → use rebase instead of fetch and merging 

_Copy all the files from a remote repository:_
```
$ git clone <repository-url> <local-directory-name>
```

_Show information on remote and local branches:_
```
$ git remote show <name-repository>
```

_Remove remote branch:_
```
$ git push <name-repository> :<branch-name>
```

_Clean up deleted remote branches:_
```
$ git remote prune <name-repository>
```

# Branches
Check in which branch we currently are.
```
$ git branch
```
-	`-d <name>` → removes the specified branch.
-	`-D <name>` → removes the specified branch even if is changes are not fully merged with another.
-	`-r` → list all remote branches.

_Create a new branch:_
```
$ git branch <branch-name>
```

_Switch to another branch:_
```
$ git checkout <branch-name>
```
-	`-b` → creates a new branch.

_Merge two branches:_
```
$ git merge <branch-name>
```
-	`--no-ff` → do not do a fast-foward merge.

For example merge a side branch to the master one. It will appear an editor for a merge message, to explain why the merge is necessary.

## Rebase
_Pulls down all changes from a remote repository, but don't merge them:_
```
$ git fetch
```

_Reapply commits on top of another base tip:_
```
$ git rebase [<upstream> [<branch>]]
```
The current branch is reset to a newbase and the commits preaviously saved into the temporary area (after excuting rebase) are then reapplied to the current branch.

When doing a rebase, it's possible conflits happen. Rebase will stop and ask you to solve that conflit. After you fix it, run `git add <file-name>` and `git rebase --continue`, so the rebase procceds.

`-i` → interactive rebase, allows changing the commits in some way. It will open an editor. After we save and exit, this will move our commits into a temporary area and then run the commands we wrote.
```
$ git rebase -i <commits-to-change>
```

Rebase alters every commit AFTER the one you specify:
- `HEAD~3` → means the last three commits.
- `HEAD^` → parent of HEAD, so last commit.
	
`pick` → run commit one at a time, nothing is going to change. You can use it to switch the order of the commits with this.\
`reword` → change commit message.\
`edit` → edit the commits in some way. To split into 2 commits, run the file and when it gets to the edit part it will put us in the command line. We can do git reset so we roll back the changes, add the files to the staging area and commit them separately. After you are done you run `git rebase --continue` to continue running the commands.\
`squash` → merges a commit with the previous commit. It will make you write a new commit message.

# Tagging
A tag is a reference to a commit. It's used mostly for release versioning. There are three types of tags:
- __Lightweight__ → just a tag, no message or tagger;
- __Signed__ → uses public key to prove identity of tagger;
- __Annotated__ → adds info on who tagged, when and why. This is the most common one.

It's best practice to tag every time you push to production, the exception being if every commit on master goes to production. You should use the semantic versioning.

_List all tags:_
```
$ git tag
```

_Check out a specific tag, and go back to how the code looked like when we tagged it:_
```
$ git checkout <tag-name>
```

_Add a new tag:_
```
$ git tab -a <tag-name> -m "tag description"
```
-	`-s` → signed tag.
-	`-a` → annotated tag.
-	`-m` → message for the tag.

_Push our tags:_
```
$ git push --tags
```
If we don't push it, the tags will just remain local.

# History
_Look at the commits' history:_
```
$ git log
```
-	`--pretty=oneline` → display one commit per line.
-	`--pretty=format:"<format>"` → format the output as specified using the placeholders. Run git help log for more options.

Placeholder | Replaced With
--- | ---
`%ad` | author date
`%an` | author name
`%h` | SHA hash
`%s` | subject
`%d` | ref names

-	`--oneline -p` → display what each commit changed.
-	`--oneline --stat` → display how many insertions and deletions were made for each file included in each commit.
-	`--oneline --graph` → get visual representation of the branches and the commits. Useful to see the branch's merges.
	
_Compare between two commits or branches:_
```
$ git diff [commit-sha..commit-sha]
```
-	`--staged` → view staged differences

If none is specified it will compare the unstaged differences with the lastest commit.
| | |
--- | ---
`HEAD` | lastest commit
`HEAD^` | parent of lastest commit
`HEAD^^` | grandparent of lastest commit
`HEAD~5` | five commits ago

_Show all changes of specified file in each line, who made them, when, and in which commit created that change:_
```
$ git blame <file-name> --date short
```

### Specifying ranges
_Until:_
```
$ git log --until=1.minute.ago
```

_Since (days):_
```
$ git log --since=1.day.ago
```

_Since (hours):_
```
$ git log --since=1.hour.ago
```

_Since & until (relative):_
```
$ git log --since=1.month.ago --until=2.weeks.ago
```

_Since & until (absolute):_
```
$ git log --since=2000-01-01 --until=2012-12-21
```

# Cherry-Pick
Apply the changes introduced by some existing commits. Check the commit number with `git log` and change to the branch that you want to apply the commit.
```
git cherry-pick <commit>
```
That copies a single commit to the current branch.

`--edit` → lets you change the commit message. It will open an editor.
```
git cherry-pick --edit <commit>
```

`--no-commit` → pulls in changes and stages them, but doesn't commit. You have to manually commit the changes then. This can be used to combine two commits.
```
git cherry-pick --no-commit <commits...>
git commit -m "<commit-message>"
```

`-x` → adds source SHA to commit message. Only useful with public branches; don't use for local branches.
```
git cherry-pick -x <commit>
```

`--sigoff` → adds current user's name to commit message.
```
git cherry-pick --sigoff <commit>
```

# Stashing
You can store files that are not yet ready to commit in a temporary area if you need to do something else (like commiting files in another branch). Every time you push a stash you are putting your files into the stash stack, where all the stashes are. Each stash as a name that you can use to apply.

_Save files to temporary area and restore the state from the last commit:_
```
$ git stash save ["stash message"]
```
-	`--keep-index` → causes the staging area not to be stashed.
-	`--include-untracked` → causes untracked files to be stashed too.

_Bring stashed files back:_
```
$ git stash apply [<stash-name>]
```

_List all stashes in the stack:_
```
$ git stash list
```
-	`list` can take any option `git log` command can
-	`--stat` → summarizes the file changes of all stacked stashes
It shows the name of each stash and the last commit before we stashed.

_Shows information about one particular stash:_
```
$ git stash show [<stash-name>]
```
-	`show` can take any option `git log` command can
-	`--patch` → shows files diffs

_Delete a stash from the list:_
```
$ git stash drop [<stash-name>]
```

_Bring stash back and delete it from the stack_
```
$ git stash pop [<stash-name>]
```

_Creates a new branch with the stash files_
```
$ git stash branch <name-branch> <name-stash>
```
This drops the stash automatically.

_Clears all stashes from the stack_
```
$ git stash clear
```

Conflicts are possible when applying a stash, so commit or reset your local changes, as appropriate and then run the `git stash apply` again. Sometimes git will just merge the files. If you use the pop command and it merged files it won't delete the stash from the stack.

### Shortcuts
`git stash` → `git stash save`\
When you don't specify the stash name it will choose the first stash in the stack (`stash@{0}`)

# Submodules
It's basically a Git repository inside a Git repository. It's useful for when you need to share code between projects – a library,  for example. You can pull down updates easily, share changes easily and it has a independent history of the containing repository.

You create them by creating like any other git repository (`git init <project-name>`) and them you add it to the project as submodules.

_Add a submodule to project:_
```
get submodule add <submodule-repository-address>
git commit -m "<commit-message>"
git push
```
This will create a new directory with the files from the submodule and a *.gitsubmodules* file. You need to commit both of them and push it.

Submodules by default don't start at any branch, so you need to checkout to one to make changes and commits.
If you accidentally commit files of the submodule without being on any branch, you checkout to a branch and merge the commit with the current branch.
```
git checkout <branch-name>
git merge <commit-hash>
```

_Update the files of a submodule:_
```
git submodule update
```

## When cloning a project
After cloning a repository, you will need to get the submodules. Git goes through your *.gitmodules* file and automatically adds an entry to your local configuration for each submodule.
```
git submodule init
```

After the init command there isn't any files inside the submodules folders. You need to pull down the submodules. You use the update command.
```
git submodule update
```

## Pushing the submodule and the parent project
Every time you want to update the submodule files is important to push two times – one for the submodule and the other for the parent project. The parent project needs to update the reference to the latest submodule's commit. First the submodule and then the parent project. There are some ways to help:

_Abort a push if you haven't pushed a submodule:_
```
git push --recurse-submodules=check
```
Run from the parent directory.

_Push all repositories (even submodules):_
```
git push --recurse-submodules=on-demand
```
	
It's good practice to create an alias if you are working with submodules for this command.
```
git config alias.pushall "push --recurse-submodules=on-demand"
```

# Writing Good Commit Messages
First and foremost, you should follow the conventions defined by the team you are working with. The commit message should be clear and meaningful. A well-crafted Git commit message is the best way to communicate context about a change to other developers working on that project, and indeed, to your future self.

A great template of a good commit message, written by Tim pope:
```
Short (50 chars or less) summary

More detailed explanatory text, if necessary. Wrap it to about 72 characters or so. The blank line separating the summary from the body is critical. Write your commit message in the imperative: "Fix bug" and not "Fixed bug".

Further paragraphs come after blank lines.

- Bullet points are okay too.

If you use an issue tracker, add a reference(s) to them at the bottom:

Resolves: #123
```

You can also specify the type of commit:
1. `feat`: the new feature you're adding to a particular application.
2. `fix`: a bug fix.
3. `style`: feature and updates related to styling.
4. `refactor`: refactoring a specific section of the codebase.
5. `test`: everything related to testing.
6. `docs`: everything related to documentation.
7. `chore`: regular code maintenance.

You can also use emojis to represent commit types.

# Sources
[Code School: Git Real](https://www.pluralsight.com/courses/code-school-git-real)\
[Code School: Git Real 2](https://www.pluralsight.com/courses/code-school-git-real-2)\
[How to Write Good Commit Messages: A Practical Git Guide - FreeCodeCamp](https://www.freecodecamp.org/news/writing-good-commit-messages-a-practical-guide/)