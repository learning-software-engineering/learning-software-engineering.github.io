# `git merge` vs. `git rebase`

Both `git merge` and `git rebase` are methods for integrating new commits that are on separate branches. However merging is usually what is taught in CSC207, and many students have never heard of rebasing, or have had very little experience with it. Here are some resources to get you started with learning about rebasing and the difference between the two commands!
1. [Git Basics: Merge and Rebase](https://www.youtube.com/watch?v=dO9BtPDIHJ8&ab_channel=EnvatoTuts%2B) (YouTube video) 
    
    This is a very short introduction on merge vs rebase. It goes over the most basic differences between them and provides a short example of a workflow that uses merge and a workflow that uses rebase. This is a good starting point, but you will likely need to visit the below resources as well to deepen your understanding. It can also be good video to return to if have learned this in the past and need to refresh your memory.

2. [Learn Git Rebase in 6 minutes // explained with live animations!](https://www.youtube.com/watch?v=f1wnYdLEpgI&ab_channel=TheModernCoder) (YouTube video)
    
    This video also goes over the differences between merge and rebase, but it goes into much more depth than the previous video. In particular, it provides a  detailed demo of a workflow that uses `git rebase` that models real world scenarios well. If you would like to try implementing rebasing in your workflow, the Demo section of this video will be helpful for that.

3. [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) (Atlassian article)
    
    If you prefer to read an article over watching a video, this is the resource for you, as it covers all of the topics that the above two videos cover. It also covers more scenarios that you may find yourself in while using rebase as part of your workflow. In particular, the section called [The Golden Rule of Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) will help you make sure that you don't accidentally bring catastrophe upon your repository while using rebase. Additionally, there is a short section on interactive rebase, a powerful tool that give you control over your branch history. 


# A primer on `git merge` and `git rebase`

One of the most useful features that Git introduced was *branching*. This is the cornerstone of how collaboration is done in Git, but one of the complications is when you want to reconcile the changes made in one branch with the work done in another branch. 

You may be familiar with the most common use case: you want to update your branch with the latest changes from `main`.

There are two different ways of combining two branches: merging and rebasing. They work quite differently, and we’ll explore when and why you’d choose one over the other.

## Merging

The first and classic way to combine the work done in two branches is to *merge* the two branches together. Merging is usually the default way to reconcile changes between branches because it preserves commit history (and is thus “safer”), and resolving merge conflicts is (relatively) simple compared to rebasing.

Say you are currently checked out into the `feature` branch, and you want to merge your commits in that branch into the `main` branch.

Your `feature` branch branched off of the `main` branch at some commit. We’ll illustrate the commits in chronological order (so commit B was committed after commit A).

We’ll say that feature branched off of `main` at some commit C.

So, your `main` branch may look like:
> A -> B -> C -> E -> F

And, your `feature` branch may look like:
> A -> B -> C -> D -> G

But notice that there are commits in main that happened after feature was branched off. These are commits E and F. We want to merge the changes made in those commits into `feature`; perhaps they are useful for the work we’re doing in `feature`. 

What we’ll do is merge `main` into `feature`. This firstly creates a merge commit in `feature` which incorporates all of the changes made in `main` but not in `feature` by comparing their *diffs*. Any changes made in `main` but not `feature` are then applied to `feature` via the merge commit.

Then, in the Git log, you’ll see that the commits in these two branches are preserved, but they then converge with the merge commit.

So, `feature` now has both the commits of `main` and itself, so it is “up to date” with `main`:
> Feature branch:
>
> A -> B -> C -> E -> F -> (merge commit)
>
>             ↳ D -> G -> ⬏

## Rebasing

As you saw, merging does not hide the fact that `feature` and `main` were being worked on in parallel. But, you might have noticed that another way of importing commits E and F into `feature` would be to change the commit that `feature` branched off of `main` from commit C to commit F. 

Recall that the `main` branch looks like:
> A -> B -> C -> E -> F

And the `feature` branch look likes:
> A -> B -> C -> D -> G

Merging resulted in a branch that looked like:
> A -> B -> C -> E -> F -> (merge commit)
>
>             ↳ D -> G -> ⬏

But, wouldn’t it be nice if `feature` could look like:
> A -> B -> C -> D -> E -> F -> G

In a nutshell, we pretend that `feature` didn’t actually branch off at commit C, and instead branched off at the latest commit of `main`: commit F. You have just described rebasing!

Rebasing is when you change the commit at which a branch was branched off from another branch. 

So, in our example, we are rebasing `feature` on `main`, because we are changing the base commit, or “rebasing” `feature`. 

You can visualize this as detaching every commit in `feature` after commit C (the last commit that `main` and `feature` share) and appending them to the end of `main`. Then, this new branch becomes the rebased version of `feature`.

An important note to make is that each commit is “moved” one-by-one, therefore unlike merging, you can actually encounter multiple merge conflicts while rebasing. 

Rebasing comes with a big advantage though: it creates an entirely linear history after the rebase because it acts as if the branch that is being rebased was created after the latest commit of the branch being rebased on. This may not seem like such a big deal, but when you’re trying to track down what commit caused a certain bug, you will be wishing that your git history was linear!

Doesn't this:
> A -> B -> C -> D -> E -> F -> G

Look better than this?
>
> A -> B -> C -> E -> F -> (merge commit)
>
>             ↳ D -> G -> ⬏



### A small warning

You should take care with rebasing if you’re working with a remote repository! Rebasing is rewriting history, and as a general rule, rewriting history is dangerous when done on a branch that multiple people work on. However, if you are the only person working on that branch, rebasing is harmless if you know what you are doing.

The general advice is that you should only rebase branches that you are working on by yourself. If you expect multiple people to be working on a branch, you should stick to merging. You may also find that when two branches have diverged for a long time, rebasing may cause you to need to solve many rounds of merge conflicts, while merging requires only 1 round of merge conflicts (remember the merge commit?).

## `git rebase --interactive`

While git rebase is used for rebasing a branch on another branch, we can also edit the commits before they are applied using the --interactive flag. In most cases though, we use `git rebase --interactive` on the currently checked out branch.

This sounds a bit scary, but what it essentially boils down to is that you can rewrite history at will! Want to squash two commits into one? Or maybe drop a commit that you made two months ago? Or maybe swap the order of two commits? Interactive rebase gives you all these powers.

In this section, we’ll cover the most common operations: pick, reword, edit, squash, fixup, and drop.

To start an interactive rebase, use `git rebase --i <commit hash>`, where <commit hash> is the last commit hash you DON’T want to modify (i.e. your base commit).

When you start an interactive rebase, you’ll be met with a log of the commits you’ll be rebasing (oldest commits at the top).

By default, each commit has “pick” to its left, which means Git will simply add that commit as-is.

- To change the order of your commits, copy-paste your commits into the order you want.
- To change a commit’s message, replace “pick” with “reword”.
- To squash a commit into the previous commit, replace “pick” with “squash”.
- To squash a commit into the previous commit but use the previous commit’s message, replace “pick” with “fixup”.
- To drop (i.e. delete) a commit, replace “pick” with “drop”.
- To edit or split up a commit, replace “pick” with “edit”.

Once you’ve decided on your actions, save and exit the editor, and the rebase will begin. Remember that Git is applying your commits top-down, and so any conflicts that occur need to be solved on a commit-by-commit basis! If you get regrets on the rebase, you can cancel at any time with `git rebase --abort`, which will undo everything done during the rebase.

If you used “reword” or “squash”, Git will open an editor for you to decide on the commit message. Simply type in the message you want, then save and exit the editor.

If you used “edit”, Git will pause execution at your commit, and you should go ahead and make your changes. If you want to edit your commit, use `git add` and `git commit --amend`, and if you want to split your commits, use `git reset HEAD^` to do a mixed reset of your commit, then use `git add` and `git commit` to make new split-up commits. Finally, when you’re done editing, simply use `git rebase --continue` to move onto the next commit to rebase.

When every commit has been applied, the rebase should automatically end, and you should have the changes you wanted!
