
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

To see all the command and one line

```
git log -all --oneline
```

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

### git reset (Data lose)

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

if you want to return to `67f4ef8c7515a58476f804e0c276f0b0dd6d8110` and delete after code permanently use

```
git reset --hard 67f4ef8c7515a58476f804e0c276f0b0dd6d8110
```


### git revert (No Data lose)

If you don't want do delete present commit but go back to last commit You should use

```
┌──(azam㉿kali)-[~/Desktop/prac]
└─$ git log --oneline      
2150c6d (HEAD -> master) Droppy
d13ebc2 jerry
d85e24a TOM
                                                                       
┌──(azam㉿kali)-[~/Desktop/prac]
└─$ git revert 2150c6d
[master bc93c93] Revert "Droppy"
 1 file changed, 1 deletion(-)
                                                                       
┌──(azam㉿kali)-[~/Desktop/prac]
└─$ git log --oneline 
bc93c93 (HEAD -> master) Revert "Droppy"
2150c6d Droppy
d13ebc2 jerry
d85e24a TOM
```

You should use present hash

If you now want to see/use Droppy use

```
git checkout 2150c6d
```

## Git branch

To see local branch

```
git branch
```

To `create a new branch` we will use branch name as `new`

```
git branch new
```

To go another branch name `new` 

```
git checkout new 
```

OR

```
git switch new
```

To delete branch 

```
git branch -d new
```

## Merge branch

To merge `new` branch with `master` branch , you should first go to `master` branch and then use the command

```
git merge new
```

Another way is 

```
┌──(azam㉿kali)-[~/Desktop/prac]
└─$ git log --all --oneline
5c6a103 (fi1) add another file
4736e57 reslove conflict
c180ea6 added a of question
b455f89 (HEAD -> fi2) added a lin in f1.txt
4b8e62a (master) Merge branch 'fi2'
7a26ae3 add ext2.txt
901b0d7 add ext1.txt
ddbbc73 add f1 f2 f3 text file
```

Now we will take `5c6a103 (fi1) add another file` commit to `fi2` branch. After going `fi2` branch we will use this command

```
git cherry-pick 5c6a103
```

This command make a new commit in `fi2` branch
### Git Conflict & Resolution

A **Git conflict** happens when Git can’t automatically merge changes from different branches or commits.

This usually happens when:

- Two people change the same lines in a file.
    
- A file is deleted in one branch but modified in another.
    
- You try to merge, rebase, cherry-pick, or pull.

#### 🔥 Example of a Conflict

Two branches (`main` and `feature`) both edited the same line of `index.html`.

```
<<<<<<< HEAD
<h1>Hello from main</h1>
=======
<h1>Hello from feature</h1>
>>>>>>> feature
```

#### 🔧 How to Resolve a Git Conflict

### Step-by-Step

1. **Trigger the conflict**  
    (e.g., run `git merge feature` from `main`)
    
2. **See the conflict**  
    Git will show:
```
CONFLICT (content): Merge conflict in index.html
```
    
3. **Open the conflicted file**  
    You’ll see this format:
    
```
<<<<<<< HEAD
Your code (main branch)
=======
Incoming code (feature branch)
>>>>>>> feature
```
    
4. **Edit the file manually**  
    Decide what to keep, delete conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), and save.
    
5. **Mark as resolved**
    
```
git add <conflicted-file>
```
    
6. **Commit the merge**
    
```
git commit
```


#### 🧠 Useful Commands Summary

| Command             | Description               |
| ------------------- | ------------------------- |
| `git status`        | Check what’s in conflict  |
| `git diff`          | See differences in files  |
| `git log --merge`   | See conflicting commits   |
| `git merge --abort` | Cancel a bad merge        |
| `git add <file>`    | Mark conflict as resolved |
| `git commit`        | Finish the merge          |