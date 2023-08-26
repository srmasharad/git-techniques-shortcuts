# Git Techniques & Shortcuts

### Committing

#### Commit
```bash
git commit -am "YOUR_COMMIT_MESSAGE"
```
###### *Note: Use `-am` if you don't have new files. This is the shortcut for add and commit together.*

#### Create an Alias for Commit
```bash
git config --global alias.ac "commit -am"
git ac "notice!"
````

#### Ammend the Last Commit Message
```bash
git commit --amend -m "nice!"
````

#### Ammend the Last Commit and Add Files
```bash
git add .
git commit --amend --no-edit
````
###### *Note: `--no-edit` keeps the same commit message. Keep in mind that it really works if you have already pushed your code in remote repositories*

#### Force Push to Overwrite Remote History
```bash
git push origin master --force
```

#### Revert a Commit with a New Commit
```bash
git revert <commit_sha>
```
###### *Note: If you feel the file shouldn't be there in repositories like it's garbage*

### Stash
Stash will remove the changes from your current working directory and save them for later use without committing them to the repo.
```bash
git stash
git stash pop
```
###### *Note: Do `git stash pop` when you're ready to add those changes back into your code*.

But if you use commands a lot
```bash
git stash save "write a name to reference it later"
```
Then when you are ready to work on it again use
```bash
git stash list
git stash apply 0
```
###### *Note: 0 is the corresponding index to use it*.

#### Change Default Branch Name
```bash
git branch -M <new_branch_name>
```

#### Go to Previous Branch
```bash
git checkout -
```

#### Delete Branch from Local & Remote
```bash
git branch -D <branch_name> && git push -d origin <branch_name>
```

### Git Log Visualization
#### Log
The problem with this command is that the output is harder and harder to read as your project grows in complexity.
```bash
git log
```
To make the Git log more readable and concise, use:
```bash
git log --graph --oneline --decorate
```
You can now see a more concise breakdown and how different branches connect together. But if you're looking at the git log there's likely a commit in there that's currently breaking your app.

### Git Bisect
 Allows you to start from a commit that is known to have a bug likely the most recent commit but you knew that the app was working a few hours ago.
 ```bash
git bisect start
```
###### *Note: Point to the last known working commit then it performs a binary search log to walk you through each commit*

```js
git bisect bad
// If the commit looks good type
git bisect good 6d010fd // to move on to the next commit eventually
```
### A new technique that every developer should know is how to squash their commits.
#### Squash

Imagine you're working on a feature branch that has three different commits and you're ready to merge it into the master branch (i.e.`main` branch) but all these commit messages are kind of pointless and it would be better if it was just one single commit we can do that from our feature branch by running.
```js
git rebase master --interactive // This will pull up a file with a list of commits on this branch
```
For more productivity, you can also use
```bash
git commit --fixup fb2f677
git commit --squash fc2f55
```
For JavaScript Developer there's a package called [Husky](https://typicode.github.io/husky/) that makes it much easier.

### Destruction

Let's imagine you have a remote repository on github than a local verssion on your machine that you've been making changes to but things haven't been going too well and you just want to go back to the original state and the remote repo.

#### 1. First do
```js
git fetch origin // to grab the latest code in the remote repo
git reset --hard origin/master // to override your local code with remote code
```
###### *Note: But be careful your local changes will be lost forever*

## Forking and Pull Requests

#### Step 1 
Fork the repo
#### Step 2:
Clone the repo from your github using https or ssh and rename the origin name.
```bash
git@github.com:YOUR_USERNAME/REPO_NAME.git
```
Rename it with your own name or organization name during clone
```bash
git@NAME_ANY.github.com:YOUR_USERNAME/REPO_NAME.git
```
###### *Note: NAME_ANY must be organization name or your name to meet the standard.*

#### Step 3: 
Ater clone is completed check the upstream using `git remote -v`. If you see origin and upstream both then you can start working in your project creating new branches.

#### Step 4:  
If upstream is not added then add upstream using 
```bash
git remote add upstream <original_repo_url>
```
You can see the upstream is added. To check type `git remote -v`. Also you can do
```bash
git fetch upstream <original_repo_url>
```
#### Step 5:  
If you forget to rename the link during clone just do following:
```bash
git remote add one <your_repo_url>
git pull one main
```
Once you added the `one` remove the `origin` using 
```bash
git remote rm <name_of_origin>
```
After remove the origin, rename `one` with name `origin` using 
```bash
git remote rename origin
```
#### Step 6:
If you are in any active branch to pull the changes from `upstream` use 
```bash 
git fetch upstream main
```
To merge the changes use 
```bash
git merge usptream/main
```
This will merge the changes of `upstream` main to your local branch which you are working in.

Also you can merge without checkout from the current branch using 
```bash
git fetch upstream main
git pull upstream main:main
```
This will merge `upstream` main branch into your local `main` branch without checkout to `main`.

###### *Note: Your current branch also updated using recursive method by git.*

#### Step 7: 
To push your branch and create a PR 
```bash
git push origin <your_branch_name>
```
This wil open the PR for your branch.

#### Step 8: 
To keep your `origin` sync with `upstream` 
```bash
git push origin main:main
```
This will synck fork and keep your origin main branch updated with upstream main. 

###### *Note: only do this when your `upstream` main and local `main` are equally sync or updated*


