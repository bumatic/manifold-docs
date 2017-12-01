# Resolving merge conflicts

Sometimes when you want to merge or rebase your branch into the master branch, you'll run into a conflict. Conflicts happen when you've changed files in your branch that have also been changed by someone else in the master branch. In some cases, Git can resolve the conflict on its own. But if you're both editing the same file in the same spots, the computer needs a human to tell it which changes should be applied.

One way to avoid conflicts is to keep your branches small and current. Before you start a new set of changes, make sure you've pulled the master branch, and then create your branch off of the current master (`git checkout master` follow by `git pull origin master` followed by `git checkout -b zd/my-branch`). Conflicts are more likely to arise in branches that have been around for a long time and that haven't been regularly rebased onto master. That said, resolving conflicts isn't as big a deal as it sounds.

For this example, I'll look at the `ts/edp-workflow` branch, which currently has a conflict with the master branch. Let's take a look at the two branches:

```
zdavis@gelatinous-cube:~/src/manifold-docs$ git branch
  master
* ts/edp-workflow
  zd/install-instructions
  zd/webhook
```

I've confirmed I'm in the right branch. Now let's compare it to master.
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git show-branch ts/edp-workflow master
* [ts/edp-workflow] Updates/rename of contents/presses/workflow
 ! [master] [C] Undo minor change to test webhook
--
 + [master] [C] Undo minor change to test webhook
 + [master^] [C] Apply minor change to test webhook
 + [master~2] [C] Trivial commit to test webhook - #2
 + [master~3] [C] Trivial commit to test webhook - #1
 + [master~4] Removing redundant Proposal section from contents\presses
 + [master~5] Updates to contents\authors\rights
 + [master~6] beginning to fill in reader documentation. first rough draft.
*  [ts/edp-workflow] Updates/rename of contents/presses/workflow
*+ [master~7] Updates to contents/authors/project_proposals
```

Again, reading the show-branch ouptut takes some practice. Here I can see that the ts/edp-workflow branch converges with master 8 commits back. Here's a rough visualization of this:

```
            _ ts/edp-workflow
           /
~9 - ~8 - ~7 - ~6 - ~5 - ~4 - ~3 - ~2 - ~1 - master
```

We want to take the commit in ts/edp-workflow and tack it onto the end of the master branch, which means we need to rebase ts/edp-workflow onto master.

```
zdavis@gelatinous-cube:~/src/manifold-docs$ git rebase HEAD master
First, rewinding head to replay your work on top of it...
Applying: beginning to fill in reader documentation. first rough draft.
Applying: Updates to contents\authors\rights
Applying: Removing redundant Proposal section from contents\presses
Using index info to reconstruct a base tree...
M	SUMMARY.md
Falling back to patching base and 3-way merge...
Auto-merging SUMMARY.md
CONFLICT (content): Merge conflict in SUMMARY.md
error: Failed to merge in the changes.
Patch failed at 0003 Removing redundant Proposal section from contents\presses
The copy of the patch that failed is found in: .git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
```

This message tells us that there is a conflict. In this case, I changed SUMMARY.md, and so did one of those commits in master. My rebase can't be finished until I address this conflict. If I type `git status`, I can see that I'm in the middle of a rebase:

```
zdavis@gelatinous-cube:~/src/manifold-docs$ git status
rebase in progress; onto 4828e6a
You are currently rebasing branch 'master' on '4828e6a'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

	both modified:   SUMMARY.md

no changes added to commit (use "git add" and/or "git commit -a")
zdavis@gelatinous-cube:~/src/manifold-docs$
```

Let's see what's up with that file:
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git diff SUMMARY.md
diff --cc SUMMARY.md
index fda639f,cb4ffd7..0000000
--- a/SUMMARY.md
+++ b/SUMMARY.md
@@@ -14,8 -14,7 +14,12 @@@
    * [Digital Services](contents/getting_started/digital-services.md)
  * [Presses](contents/presses/README.md)
    * [Project Types](contents/presses/project_types.md)
++<<<<<<< HEAD
 +  * [Proposals](contents/presses/proposals.md)
 +  * [Editorial and Production Workflow](contents/presses/workflow.md)
++=======
+   * [Editorial & Production Workflow](contents/presses/editorial_and_production_workflow.md)
++>>>>>>> Removing redundant Proposal section from contents\presses
    * [The Backend](contents/presses/the_backend/README.md)
      * [Projects](contents/presses/the_backend/projects/README.md)
        * [General](contents/presses/the_backend/projects/general.md)
```
It looks like in HEAD (the feature branch) we changed the path to "Editorial and Production Workflow". In another commit that's already in master, we removed the proposal section. These changes are too close, so we need to open the file and fix this.

We'll see the diff in the file when we open it:

```
* [Presses](contents/presses/README.md)
  * [Project Types](contents/presses/project_types.md)
<<<<<<< HEAD
  * [Proposals](contents/presses/proposals.md)
  * [Editorial and Production Workflow](contents/presses/workflow.md)
=======
  * [Editorial & Production Workflow](contents/presses/editorial_and_production_workflow.md)
>>>>>>> Removing redundant Proposal section from contents\presses
  * [The Backend](contents/presses/the_backend/README.md)
    * [Projects](contents/presses/the_backend/projects/README.md)
      * [General](contents/presses/the_backend/projects/general.md)
```

I'll change it to look like this:

```
* [Presses](contents/presses/README.md)
  * [Project Types](contents/presses/project_types.md)
  * [Editorial and Production Workflow](contents/presses/workflow.md)
  * [The Backend](contents/presses/the_backend/README.md)
    * [Projects](contents/presses/the_backend/projects/README.md)
      * [General](contents/presses/the_backend/projects/general.md)
```

Then I add go ahead and stage the modified file to tell Git that I've resolved this conflict:

```
zdavis@gelatinous-cube:~/src/manifold-docs$ git add SUMMARY.md
zdavis@gelatinous-cube:~/src/manifold-docs$ git status
rebase in progress; onto 4828e6a
You are currently rebasing branch 'master' on '4828e6a'.
  (all conflicts fixed: run "git rebase --continue")

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   SUMMARY.md
```

Notice that git tells me that I've now addressed all conflicts, so it can continue with the rebase. Great, let's proceed:
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git rebase --continue
Applying: Removing redundant Proposal section from contents\presses
Applying: [C] Trivial commit to test webhook - #1
Applying: [C] Trivial commit to test webhook - #2
Applying: [C] Apply minor change to test webhook
Applying: [C] Undo minor change to test webhook
```
At this point, the rebase has completed. Let's compare the branch to master:
```
zdavis@gelatinous-cube:~/src/manifold-docs$ git show-branch HEAD master
! [HEAD] [C] Undo minor change to test webhook
 * [master] [C] Undo minor change to test webhook
--
+* [HEAD] [C] Undo minor change to test webhook
```

All right, my commit is now on the tip of the master branch. Time to push my feature branch to Github with `git push origin ts/edp-workflow -f`. Notice that I'm force pushing here with the -f flag. By rebasing, I've changed the history of my branch. It's necessary to force push an update version, which overwrites the old version on Github. You should never do this with the master branch, because we all share that branch. In the case of a feature branch, however, it's fine, because you're not really sharing it with other contributors.

Once the branch is pushed, the conflict on github will be gone, and the branch can be cleanly rebased onto master.



