# [Bandit Level 28 → Level 29](https://overthewire.org/wargames/bandit/bandit29.html)

## Goal
There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo via the port 2220. The password for the user bandit28-git is the same as for the user bandit28.
Clone the repository and find the password for the next level.

## Theory
Git commads used in this task.
1. `git log` - Show commit logs. More information [here](https://git-scm.com/docs/git-log).
2. `git show` - Show various types of objects, we need this to check more information about a particular commit. More information [here](https://git-scm.com/docs/git-show).

What are commits?
Commits can be thought of as snapshots or milestones along the timeline of a Git project. Commits are created with the git commit command to capture the state of a project at that point in time.

## Solution
1. Start with creating a temp folder and cloning the repo just as the last task.
```
bandit28@bandit:/tmp/tmp.z99nzRmyLa/repo$ ls -la
total 16
drwxrwxr-x 3 bandit28 bandit28 4096 Apr 16 12:50 .
drwx------ 3 bandit28 bandit28 4096 Apr 16 12:50 ..
drwxrwxr-x 8 bandit28 bandit28 4096 Apr 16 12:50 .git
-rw-rw-r-- 1 bandit28 bandit28  111 Apr 16 12:50 README.md
```
2. Open the `README.md` file.
```
bandit28@bandit:/tmp/tmp.z99nzRmyLa/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```
3. Instead of password, we have `xxxxxxxxxx`. Use `git log` to see what changes have been made to this repo.
```
bandit28@bandit:/tmp/tmp.z99nzRmyLa/repo$ git log
commit 674690a00a0056ab96048f7317b9ec20c057c06b (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Apr 10 14:23:19 2025 +0000

    fix info leak

commit fb0df1358b1ff146f581651a84bae622353a71c0
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Apr 10 14:23:19 2025 +0000

    add missing data

commit a5fdc97aae2c6f0e6c1e722877a100f24bcaaa46
Author: Ben Dover <noone@overthewire.org>
Date:   Thu Apr 10 14:23:19 2025 +0000

    initial commit of README.md
```
4. The first commit with the message 'fix info leak' looks interesting. Use `git show` to see what was changed in this commit.
```
bandit28@bandit:/tmp/tmp.z99nzRmyLa/repo$ git show 674690a00a0056ab96048f7317b9ec20c057c06b
commit 674690a00a0056ab96048f7317b9ec20c057c06b (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Apr 10 14:23:19 2025 +0000

    fix info leak

diff --git a/README.md b/README.md
index d4e3b74..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
+- password: xxxxxxxxxx
````
5. And here we see that the line 'password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7' was changed to 'password: xxxxxxxxxx' and we have our password.
