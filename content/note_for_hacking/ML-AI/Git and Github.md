



# Starting

## Config file edit

Set user name and email

```
git config --global user.name "emamulazam"
git config --global user.email "e**********@gmail.com"
```

Edit config file

```
git config --global -e
```

## Start basic git

Initialize git command

```
git init
```

To show status **(To see any file status of the repository)**

```
git status
```

if there have any `untracked files` to track the file use **(non staging area to staging area)**

```
git add <file name> <file name> ...... <file name>
```

If you want to add all the files at once then use

```
git add .
```

**Now git know about the file you add. But at this point git don't take snapshot**

To take a snapshot / track the files you add you should `commit`

If you make commit a line comment

```
git commit -m "comment"
```

If the commit have more then one line comment then write the flowing command and then write your comment and then exit the text editor

```
git commit
```

To see the commit you done write the command

```
git log
```

To remove git repository

```
rm -rf .git
```

## More command with `git init`

Initialize git repository with a name like `main`

```
git init --initial-branch=main
```

# Undo git add

If you want add some unnecessary file and now you want to undo the **git add** then

```
git rm --cached <file name>
```

