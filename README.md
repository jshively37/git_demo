# GIT Demo

This is a simple walkthrough of basic operations of git.

The first step is going to be clone down the repository and change into the directory.

```bash
git clone https://github.com/jshively37/git_demo.git
cd git_demo
```
As you can see the folder structure is identical and a ```git status``` shows up to date.

We can create a file called ```hello_world.py```

```bash
vi hello_world.py
```

In this file add:

```python
print('Hello World!')
```

If we do a git status we see untracked files. This means we have changes to our working directory that GIT is unaware of.

To tell git it needs to track these files we can issue:
```bash
git add hello_world.py
```
If you have multiple files you can also do a ```git add .```

If we do a ```git status``` again you will see that it has changed from untracked files to changes to be committed.

Let us create another file and call it ```passwords.txt``` and do a ```git add .```

If you accidently stage a file that has sensitive data or data that should not be committed you can issue a
```bash
git reset HEAD passwords.txt
```

This moves the file from staging back to working.

One option would be to tell git just to ignore these files and to do that you can use a .gitignore file.

```bash
vi .gitignore
```

If we add in passwords.txt and save we now see that a git status no longer shows tracking for passwords.txt but the file is still there.

To commit these files you issue a
```bash
git commit -m "update gitignore and adding hello_world"
```
Now a git status shows we are ahead of the master branch. This is because a commit is to the local repo not the remote repo. To get our changes up to the remote repo we will issue a ```git push```

Now if we go to our remote repo we will notice that the two new files are there. A git status also shows that the branch is up to date.

That is the basics for adding, committing, and pushing. However we have not even scratched the surface of git.

We are goign to make some changes to ```hello_world.py``` and the application is no longer going to run.

Run the program and see the error.

First let us see what changed by doing a ```git diff```

Thanks to git's amazing memory we are able to recover the file from the local repo's last commit.

To do that type in ```git checkout -- hello_world.py```

```git diff``` shows no changes and a ```git status``` shows back to clean working branch.

If the file accidently got added to the staging area (shame on you for not testing your code before staging but it happens). We will just do the same thing we did with the passwords.txt file and do a git reset HEAD hello_world.txt and then issue a git checkout -- hello_world.txt.

If you accidently committed the file fear not you can still recover.

Break the file again
```git commit -am "Bad"```

The -am tells it to add all the files and commit them. It is a shortcut way of doing a git add and commit

We need to find the hash we want to back from:

```git log --all --decorate --oneline --graph``` and this will show you the status.

Find the hash of the commit you want the file from and then you can issue.

```git checkout (hash) -- (filename)```

For example for us we want to back up to the previous commit so we would do:
```git checkout e710da1 -- hello_world.py```

Another very powerful feature of git is branching. I use them constantly because it allows me to keep my master branch as what I expect and then allows me to add features/bugfixes/etc. There are ways to do this locally, push the branches to the remote repo, etc. but if there is interest we can do another session that gets more into intermediate/advanced git operations (we still have not even scratches the surface).

The easy way is just go to the webpage and create a branch from there. We notice both branches have hte same commit hash so we know they are in sync.

If we go to our PC and try and checkout this branch we are goign to get an error.

If we do a ```git branch -a``` we see that new branch is not on our local yet.

This is because we need to tell our local repo to check the remote repo for any changes. To do this we do a ```git pull```

If we do a ```git branch -a``` we see a new branch is available and now we can check it out.

```git checkout hello_world2```

A ```git branch -a``` shows we are on the hello_world2 branch.

Now let us add another file called ```hello_world2.py``` with a little bit more information.

Let us cheat and do the ```git add .``` and ```git commit -m "Hello World2``` and a ```git push```

We will see our branch is up to date and everything is good.

If we flip back to the webpage though we will notice only hello_world2 branch was updated and the commit hashes are different for master and hello_world2. As of now master is unaware of the changes.

If we click on the compare and pull request we can see the differences and do a pull request that will merge teh two branches.

Walk through deleting the branch.

Flip back over to your terminal and ```git checkout master```. However once again we are not goign to have the changes because we have not told our local repo to get them. To do that we will do a ```git pull -p``` and you can see new files came down. The -p also tells git to prune any branches that have been deleted from teh remote repo.

To delete the branch we can do a git branch -d hello_world2

Once again we can do a ```git log --all --decorate --oneline –graph``` to show the git log.

Also git is very nice and that git (command) --help will display help for the items.
