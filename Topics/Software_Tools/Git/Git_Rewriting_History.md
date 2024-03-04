# Rewriting History in Git

Note: This article assumes an intermediate understanding of Git.

Very briefly, Git is a version control system, which is a system that helps you keep a history of all the changes to your code repository and makes it easier to collaborate with others on that repository. Git operates using “commits”, which act like snapshots of your repository at some point in your history.

In this article, we’ll explore a more advanced topic in Git: rewriting history.

## What is Rewriting History in Git?

Have you ever been working on a piece of code, and committed it, only to realize that you went about it all wrong, and need to remove that commit? Or have you needed to make 8 fixup commits that you wished could just be squashed into one? Or maybe you’re hit by regret when you realize you can’t find the commit that introduced a certain bug due to your history being filled with so many messy cross-branch merges?

If that sounds like you, you’ll need the power of **rewriting history** in Git, where we muck with the history to make the timeline appear cleaner than it was in reality by using useful commands like `git rebase`. It’s a more advanced feature that is more dangerous than non-history-changing Git features (we might erase commits permanently!), so it’s worth learning when and how to employ this technique.

As a disclaimer, you’ll be just fine even if you never touch a single history-rewriting Git feature in your life. One of Git’s most powerful benefits, after all, is its guarantee that your entire history is saved, so your data is never lost. For example, instead of dropping a commit, you can always do a `git revert` instead, where the reverted commit still exists in your history, in case you ever want to find it again.

However, keeping your entire history is a curse in of itself: every fixup commit, each messy merge, and each reverted commit can pollute your project history with needlessly complex histories that, very likely, no one really cares about. In particular, understanding the big-picture evolution of your code repository becomes impossible—if you wanted to see why a certain feature was implemented the way it was, tracing its history from its feature branch becomes impossible when it’s littered by a ton of messy cross-branch merges and a billion fixup commits, when it could be totally avoided by doing some strategic rebasing and a fast-forward merge.

In short, changing history is a huge tool when it comes to keeping your Git history linear—it makes `git bisect` far easier, it allows you to view your history chronologically which makes understanding others’ code easier, and it avoids merge conflicts when you try to `git revert` or `git cherry-pick` from changes that came from cross-branch merges.

And your history just looks prettier. You may not even need a better reason than that.

## How Do You Rewrite History?

### A Word of Warning: Commits are Overwritten

Whenever you rewrite history in Git, you actually **overwrite** commits you have already made. This means that even if you think you're modifying a commit, you're actually replacing that commit with a new one, and deleting the old one.

This means you get a new commit hash, and the new commit will be unrecognizable from any person who pulled the old commit. This causes Git to think that your histories have diverged, which will huge issues when merging. So, unless you know what you're doing, you should only rewrite history **before** you pushed your changes to the remote repository.

### Changing the Last Commit: `git commit --amend`

The most common and easiest history-rewriting command: `git commit --amend`.

`git commit --amend` will take your staged changes and merge them with the previous commit. This replaces the previous commit.

If you want to keep the old commit message, use:
```
 git commit --amend --no-edit
```

If you want to replace the old commit message, use:
```
 git commit --amend -m “<commit message here>"
```

Remember, this only affects the very last commit you made. If you want to fixup an older commit, you'll need the power of `git rebase`!

### Discarding the Last Commits: `git reset`

Git’s reset mechanic has a couple of modes that provide different use-cases: if you want to drop, squash, or remove (but keep the changes) from the last couple of commits, then `git reset` is the command for you.

We’ll go over 3 modes: soft, mixed, and hard. In short, soft keeps and stages the resetted changes, mixed keeps the resetted changes, and hard will remove the resetted changes.


### For Squashing Commits: `git reset --soft`

`git reset --soft` is great for you if you’re looking to remove commits, but still keep the changes that were present in those commits in your staging area. This is useful if you want to squash the last couple of commits you made into a single commit.

It will reset your HEAD to the given commit, but your local changes and the changes from those commits will remain and they’ll be staged. This means that using `git commit` right after soft-resetting will immediately re-commit the changes you just reset, since those resetted changes are still in your staging area.

### For Reformatting Commits: `git reset --mixed`

This is the default mode—if you use just `git reset`, the mode is “mixed”. The “mixed” reset is a more versatile version of `git reset --soft`. It’s great if you’re looking to reformat (e.g. split up commits, change the order of commits, etc.) the last couple of commits you made.

It will reset your HEAD to the given commit AND wipe your staging area, but your local directory is untouched. In effect, this means that it keeps your local changes and the changes from the removed commits, but they are unstaged rather than automatically staged like in the “soft” reset.

### For Dropping Commits: `git reset --hard`

This is the most dangerous one of all. This resets you to the state of the given commit, throwing away your local changes and the changes from the removed commits, so it’s great if you want to start off on a clean slate exactly at the state of the given commit.

It will reset your HEAD to the given commit, wipe your staging area, and reset your local directory. This is a reset in every sense of the word, and your changes are actually gone! Be very careful.

Remember, this is only useful if you want to reset to the state of a previous commit. If you want granular control over which commits to drop between now and some point in time, read on for the section on `git rebase`!

## Updating Remote Branches: `git push --force-with-lease`

Using any of the above commands changes your history, which isn’t a problem when you’re working on local changes, since you control what’s the truth when it’s all local.

However, using any of them on a remote branch is a problem: your history has diverged from the deployed history, so using `git push` will fail, since Git protects against diverging histories. Furthermore, any person who has your branch checked out will find that they’ll be unable to `git pull` any update you make, since their branch no longer has the same history as yours.

In short, you should try not to perform history-rewriting on branches that you’ve already pushed (unless your PR review system calls for it), since it makes everyone’s day worse.

If you’re still intent on pushing your rewritten history, then you’ll need the power of `git push --force`, or its safer version `git push --force-with-lease`.

`git push --force` will “force push” your changes to the remote branch: it completely overwrites the remote branch with your local branch, so your rewritten history becomes the new official history. A word of warning: if you have an out-of-date version of the branch (maybe your co-workers have pushed a couple of commits) and you force-push, you’ve just deleted all the changes your co-workers made!

`git push --force-with-lease` is the same as `git push --force`, but with a built-in safety feature: it will fail if the remote has new commits that you did not fetch yet. This will prevent you from accidentally overwriting your co-workers’ work!

In short, always stick with `git push --force-with-lease` if you’re looking to force-push your changes to the remote repository.
