
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

## Undo git add

If you want add some unnecessary file and now you want to undo the **git add** then

```
git rm --cached <file name>
```

## Git commit

If you changes edit a tracked file then use

```
git commit -ma "<comment>"
```

### Modify commit

#### With new message

First you should add all the files to staging area

```
git add .
```

Then user the command

```
git commit --amend
```

#### Without new message

First you should add all the files to staging area

```
git add .
```

Then user the command

```
git commit --amend --no-edit
```

### Give a sign with commit

To give a sign with commit you should use

```
git commit -sm "<comment>" 
```

### Make an empty commit

To make an empty commit

```
git commit --allow-empty -m "<message>"
```


## Git log

To see last 2 commit

```
git log -n 2
```

To see


| command                       | Work                                   |
| ----------------------------- | -------------------------------------- |
| git log --since="1 week ago"  | Show commits from the **last 1 week**  |
| git log --since="1 day ago"   | Show commits from the **last 1 day**   |
| git log --since="1 hour ago"  | Show commits from the **last 1 hour**  |
| git log --since="1 month ago" | Show commits from the **last 1 month** |

To see commit form 1st January 2025 to 31 January 2025

```
git log --since="2025-01-01" --until="2025-01-31"
```

To see commit by anther name

```
git log --author="<auther name>"
```

To see certain keyword commit in commit massage

```
git log --grep="<keyword>"
```

## Undo commit

if it is your commits

```
┌──(azam㉿kali)-[~/Desktop/prac]
└─$ git log   
commit 5724e6ab34548b47cec76e19b93f09478870bb3b (HEAD -> master)
Author: emamulazam <emamulazam04@gmail.com>
Date:   Fri Jul 25 15:48:13 2025 +0600

    commit 6

commit 67f4ef8c7515a58476f804e0c276f0b0dd6d8110
Author: emamulazam <emamulazam04@gmail.com>
Date:   Fri Jul 25 15:47:43 2025 +0600

    commit 5

commit 37c4adad4231830068640d552fbe11116385eee3
Author: emamulazam <emamulazam04@gmail.com>
Date:   Fri Jul 25 15:46:39 2025 +0600

    commit 4
```

if you want to return to `67f4ef8c7515a58476f804e0c276f0b0dd6d8110` then and changes go to staging area

```
git reset --soft 67f4ef8c7515a58476f804e0c276f0b0dd6d8110
```

You can see changes by

```
git diff --staged
```

if you want to return to `67f4ef8c7515a58476f804e0c276f0b0dd6d8110` then and changes go to non-staging area

```
git reset --mixed 67f4ef8c7515a58476f804e0c276f0b0dd6d8110
```

Then you can see by using 

```
git status
```


