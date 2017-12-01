## Manifold Documentation Git Workflow

### Navigating in the command line

```
# change directory
cd
# list contents of current directory
ls
# prints what directory you're currently in
pwd
# go up one directory in the file system
cd ..
```

### Typical Workflow

Open a terminal, navigate to the local repository (your path will be different)
```
cd ~/src/manifold-docs
```

Check the status of your git repository
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git status
On branch master
nothing to commit, working tree clean
```

I don't have any changed files, so my working tree is clean. Before I start working, I'll fetch the remote repo to make sure I have current copies of all the branches
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git fetch --all
Fetching origin
```
Fetching doesn't change my local branches or my working tree. My local repo keeps copies of remote branches, and fetching updates those remote copies.
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git branch -a
* master
  ts/edp-workflow
  zd/webhook
  remotes/origin/jk/readers
  remotes/origin/master
  remotes/origin/ts/edp-workflow
  remotes/origin/ts/project-proposal
  remotes/origin/ts/rights
  remotes/origin/ts/some-feature
  remotes/origin/zd/webhook
```
As you can see, I have my local `master` branch in my repo, but I also have a copy of the `master` branch on github, which I can reference as `origin/master` when I'm dealing with branches.

Now that my copy of the remote (github) master branch is current, I want to rebase my master branch on top of it. Rebasing isn't as complex as you might think. Take these two branches, for example:

```
My master branch (master): #A23, #8J3, #R91, #P18
The master branch on Github (remote/origin/master): #A23, #8J3, #CJ9
```

In this example, branch A has 4 commits (with made-up IDs), and branch B has 3 commits. As you can see, the commits diverge after #8J3. Presumably, what happened here was that I started woring when the master branch was on #8J3. I made a few commits (#R91 and #P18). While I did that, someone else made a commit on master (#CJ9), so our branches diverged.

If I were to rebase my changes in master onto origin/master, I would be taking my commits and placing them at the end of the master branch. We could also merge the two branches, but I prefer rebasing because it leads to a cleaner commit history. After rebasing my master onto the remote master, I'd end up with a local master that looked like this:

```
My master branch (master): #A23, #8J3, #CJ9, #R91, #P18
The master branch on Github (remote/origin/master): #A23, #8J3, #CJ9
```

The same principle applies when working with feature branches. You create a feature branch, commit some work, rebase it onto the master branch, and then open a pull request. In practice, here's what it looks like.

First, open a feature branch. The -b flag in git checkout means "create a new branch"
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git checkout -b zd/install-instructions
Switched to a new branch 'zd/install-instructions'
```

Second, make some changes. When you're done, review what changed:
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git status
On branch zd/install-instructions
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   contents/getting_started/installation/from_package.md

no changes added to commit (use "git add" and/or "git commit -a")
```

This is a good place to make sure there's nothing unexpected. Now you're going to compose your commit by staging files that have changed.
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git add contents/getting_started/installation/from_package.md
zdavis@gelatinous-cube:~/src/manifold-docs$ git status
On branch zd/install-instructions
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   contents/getting_started/installation/from_package.md

```
I added the changd file by name, but you could add everything that changed with `git add .`. Use that sparingly though, and only after you've checked to make sure you're not adding anything unintentionally.

Now it's time to make the commit:
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git commit -m "Update package installation instructions"
[zd/install-instructions dc57692] Update package installation instructions
 1 file changed, 2 insertions(+), 1 deletion(-)
 ```

 At this point, my feature branch is one commit ahead of the master branch.
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git show-branch HEAD origin/master
! [HEAD] Update package installation instructions
 ! [origin/master] [C] Undo minor change to test webhook
--
+  [HEAD] Update package installation instructions
++ [origin/master] [C] Undo minor change to test webhook
```

It takes some time to learn how to read `git show-branch`. The row with two + signs shows where the branches meet. The row above that tells me that HEAD (which always refers to the branch I'm in, in this case zd/install-instructions) has one commit that's not in master. As expected, my branch is one commit ahead of the master branch.

Now that I'm done, I push my branch to the remote repository.
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git push origin zd/install-instructions
Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 509 bytes | 509.00 KiB/s, done.
Total 6 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 4 local objects.
To github.com:ManifoldScholar/manifold-docs.git
 * [new branch]      zd/install-instructions -> zd/install-instructions
 ```

From here, I can go ahead and open a pull request on github.




