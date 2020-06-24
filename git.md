# git

## CLI
- init git: `git init`
- stage files: `git add`
	- add all changes: `git add --all`
	- add all changes in tracked files: `git add -u`
	- add some changes of a file: `git add --patch`
- commit files: `git commit`
	- add changes of all tracked files and commit: `git commit -am "messaage"` (gcam)
- push files: `git push` (gp)
- status check: `git status` (gst)
- pull file: 
	- `git pull` = git fetch + git merge
	- `git pull –rebase` = git fetch + git rebase (gup)
- store modifications and revert working dir to HEAD
	- store: `git stash` = git stash push (gsta)
	- apply changes back: `git stash pop` = git stash apply (gstaa)
	- remove stashed change: `git stash drop` (gstd)


## merge a branch into master
- assume want to merge branch named hotfix into master
- make sure local repo is up to date
	- git fetch
	- git checkout master
	- git pull
	- checkout the branch should receive the change: master
- the merge
	- git merge hotfix
		- case: fast-forward merge
			- master has not diveraged
			- merge is just pointing master to latest of hotfix
		- case: three-way merge
			- use an extra commit to tie two branches togethgit
			- merge conflict could happen
				- resolve conflicts mannaully
				- git add on files with conflicts to mark it as resolved
				- git commit to generate the merge commit
- abort a merge
	- git merge --abort
- abort after merge
	- git reset --hard HEAD~1

## rebase and merge after cherry-pick
- git checkout master
- git cherry-pick <hotfix_a_sha>
- git rebase master b
- git checkout master
- git merge b

## branch operation
- delete local branch
	- git branch -d <branch_name>
- delete remote branch
	- git push origin --delete <branch_name>


## pull request workflow
- create new local branch: `git checkout -b <branch_name>`
- push local branch to remote: `git push -u origin <branch_name>`
- create pull create on github website
- ask for review and merge
- delete local and remote branch


## workflow
- pull remote changes & then push all locally changed files
	```sh
	git pull -r --autostash # get latest code (while reserve current change)
	if conflict
		git rebase --continue
	git add .
	git commit -m
	npm test
	git push
	```
- ammend a commit with new message
	```
	git commit --amend -m 'a new message'
	```
- ammend a commit with new changes
	```sh
	git add newly_changed_file.md
	git commit --amend --no-edit
	```
- resolve a merge conflict caused by pull
	```sh
	# ... fix conflicts in editor or diff tool
	git add resolved files
	git commit
	```
- resolve a merge conflict caused by stash
	```sh
	git stash pop
	# ... fix conflicts in editor or diff tool
	git reset or git add resolved files
	git stash drop
	git commit
	```


## what is a good commit
- easy to review
- easy to revert
- easy to `git blame`
- easy to `git bisect`


- commit message standard: angular convention
  - reference: https://github.com/angular/angular/blob/master/CONTRIBUTING.md#commit
  - commit template
    ```js
    <type>(<scope>): <subject>
    <BLANK LINE>
    <body>
    <BLANK LINE>
    <footer>
    ```
  - commit messages exmaples
    ```js
    fix(release): need to depend on latest rxjs and zone.js

    The version in our package.json gets copied to the one we publish, and users need the latest of these.
    ```

    ```js
    feat(bazel): enable ivy template type-checking in g3
    ```
  - more examples
    - https://github.com/angular/angular/commits/master

- commit message standard: tw standard
  - [name][story number] <What/Why you did>
  - example:
    ```js
    [Ze][#596] feat: added some crazy new feature
    ```


## release tagging
- types of tags
	- lightweight：just pointer to commit
	- annotated
		- contain tagger name, email and date
		- tagging message
		- `git tag -a v1.4 -m "tag message"`
- list tags
	- git tag -l
- show tag details
	- git cat-file tag <tagname>
- push tags
	- push single tag: `git push origin <tag_name>`
	- push tags: `git push origin --tags`


## print git log
- commit logs: git log --date=iso --pretty=format:'"%h","%an","%ad","%s"'
- release tags: git tag -l --sort=-creatordate --format='%(creatordate:short):  %(refname:short)'