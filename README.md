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

