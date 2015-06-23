# Pro Git 2nd edition - Scott Chacon and Ben Straub. My notes

*(intended to be a continuation to begginers tutorial)*

- Checking the settings: `git config --list` 
- If you only want to check one key: `git config key`. For example `git config email` shows the email
- Git can use both SSH and HTTPS, comparison [here](https://gist.github.com/grawity/4392747)
- Ignoring files: the file `gitignore` includes the files or extensions that you don’t want to add (for example the `.a` or `.o` files). It follows this pattern:

> Lines starting with # or blank lines are ignored
> Wildcards (*, [ ], ?, -) can be used
> Finishing a pattern with / means a directory
> ! negates a directory (you tell git not to ignore that file)

(Examples of gitignore files [here](https://github.com/github/gitignore))

- `git diff` shows what you’ve changed but not staged. This can be viewed in a tool `git difftool --tool-help` shows which tools are available in your system
- Remove a file from staging area with `git rm --cached *File*`
- You can rename a file with `git mv PreviousName ActualName` instead of changing its name, removing it from the stage and adding the new file
- Undo the last commit: `git commit -- amend`. Dont't do it if you have push the changes to a remote repo
- Unstage a file: `git reset *File*`
Unmodify a file: `git checkout -- *File*`. Dangerous command! Not possible to go back
- `git remote` to see the remote servers, `-v` option to see the url
- The name you add in `git remote add` is for your reference
- Two options for pulling data from an online repo: `fetch` and then `merge` or `pull` (`fetch` + `merge`)
- Aliases: `git config --global alias.*AliasName* *CompleteLine*` (or write them down in the gitconfig file under `[alias]`). To write an alias that uses external commands start *CompleteLine* with !
- Creating a branch means that git changes the pointer `HEAD` to that branch
- Git adds flags to the files that have merge conflicts so that they can be opened manually and fixed. It’s possible to use `git mergetool` also, which is a graphical environment for resolving conflicts
- `git fetch origin` moves the local pointer to the same place the remote pointer is
- `rebase` applies the changes done to a branch to another branch. Leads to cleaner history than `merge` (linear). Danger! Only rebase in your local repo. Some problems can be solved with `git pull -rebase` if someone has rebased the remote repo

## Git on the server: 
- 4 major protocols to transfer data: local, HTTP, Secure Shell(SSH) and Git
- Linux server covered
- Steps:

	- Create bare repository: `git clone --bare my_project my_project.git` (.git extension by convention)
	- Copy bare repository on server (SSH example) `scp -r my_project.git user@git.example.com:/opt/git`
	- Now people can clone with `git clone user@git.example.com:/opt/git/my_project.git`
	- People with write access will have push access also
	```
	ssh user@git.example.com
	cd /opt/git/my_project.git
	git init --bare --shared
	```
## Tools

- [Gitweb](https://git.wiki.kernel.org/index.php/Gitweb), [Gitlab](https://about.gitlab.com/) graphical options
- Changes can be visualized using`gitk`. Documentation [here](http://git-scm.com/docs/gitk)  

## Contributing

- [Good uses when committing](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/SubmittingPatches) 
- `git diff --check` for detecting whitespace errors (whitespace at the beginning/end of the line that makes the diffs impossible to read)
- Pull request: `git request-pull origin/master *myfork*`
- Turn commits to email: `git format-patch`. The `.gitconfig` file can be set to email this patches using IMAP with no need to copy-paste. After setting this up, use `git send-email`
If the patch has been created with `diff` it can be applied using `git apply`. If you prefer testing first use `git apply --check`. It applies works in a apply all or abort all basis - all changes are applied or none. If all the patches apply without errors it won’t show any output. Changes aren’t commited by themselves. 
- If the patch has been created using `git format-patch` the process is easier: `git am`. Automatically creates commit using the info in the email
- `git diff master...contrib` compares the master and contrib branches from their common ancestor
- Branches of the Git project: master, new, pu (proposed updates) and maint (for maintenance)
- `git cherry-pick`: little rebase
- `rerere` option: records solution of merge and next time same problem appears it automatically resolves it
Creating a build number: `git describe`
- A file (.tar .zip) can be created using `git archive`

## GitHub

- GitHub markdown
- Better give HTTP than SSH, with HTTP there is no need to have a GitHub account
- Same use of @ as Twitter
- Can subscribe to changes
- Scripting GitHub & GitHub API -> octokit

## Git Tools

- `git reflog` or `git log -g` -> log of head and branches (local operation)
- Can use ^ to reference previous commits. Ex: HEAD^ is the parent of the actual commit, HEAD^2 the second parent. Also ~ can be used, but ^2 represents the grandparent
- Range selection using .. ^ or …
- Interactive commands: `git add -i`. Typing `?` shows help. Also `git rebase -i` 
- `git stash` to change branches without committing work but also without losing it. Has to be applied using `git stash apply` to be effective  
- For searching: `git grep`. Can search in any git tree
- To rewrite history dramatically: `git filter-branch`. It can remove the same file from several commits, change the email, … Better not use it if the repo is not local.
- `git reset`: the default option uncommits and unstages the changes to the position you ask; the `--hard` option also changes the working directory (dangerous). If a path (file or files) are given reset does the opposite of add - unstages things. With `--patch` option you can unstage selectively 

*(Two much advanced topics from chapter 7 for me)*

## Garbage collection: 

- `git gc`  packs objects in compressed delta format, saves space. It can be turned on automatically changing the gitconfig file: `git config --global gc.auto 1`
- `git fsck` to check health of repository
- `git prune` to delete stale parts