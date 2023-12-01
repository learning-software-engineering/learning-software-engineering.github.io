1. Git
    1. Stash
       
        `git stash`
       
       saves a change before switching to a new branch
       
        `git stash pop`
       
       applies the latest stash and deletes the stash from the stash list
       
        `git stash list`
       
       shows the list of all stashes
       
        `git stash apply stash_ID`
       
       apply the # or stash ID from the stash list
       
        `git stash drop stash_ID`
       
       deletes the stash with stash_ID from the stash list
       
       `git stash clear`
       
       deletes all stash
       
    3. Retrieve Lost Commits
       
        `gitk --all $(git fsck --no-reflog | Select-String "(dangling commit )(.*)" | %{ $.Line.Split(' ')[2] })`

        Search inside the pop up window and simply copy paste the code back
        Link: https://stackoverflow.com/questions/89332/how-do-i-recover-a-dropped-stash-in-git
       
    4. Revert Single File From Commit
       
        `git checkout [commit ID] -- path/to/file`
       
        Link: https://dev.to/lofiandcode/git-and-github-how-to-revert-a-single-file-dha
       
    5. Revert Multiple File From Commit
       
       `git reset --soft HEAD^`
       
       `git restore --staged path/to/unwanted_file`
       
        #Note: NEVER remove the "--soft" tag, because if you remove it. The reset will be a hard reset and will remove all the changed files from the commit and sometimes it will lead into lost files and you will need to go back to "1. Retrieve Lost Commits". So for a safe practice, just use the soft reset ("--soft")
       
        Link: https://stackoverflow.com/questions/12481639/remove-file-from-latest-commit

4. Pull-requests
   
    1. Update Pull-requests
       
        After pushing your commits to create a new pull request, sometimes you realize you need to change a file that is already committed on the pull request. So you would change the file, git add, commit, push it and then realize you cannot push it. The following command will help you resolve this issue.

        `git push origin master --force`

        #Note: Use with precaution because we are using the force push. So try to limit the usage of this to directly push codes to the master branch. A great alternative would be using --force-with-lease because it does not overwrite any work on the master branch if more commits are added to the master branch. (In depth comparisons of force vs force-with-lease https://itnext.io/git-force-vs-force-with-lease-9d0e753e8c41)

3. Fetch-requests
   
   The git fetch command downloads commits, files, and refs from a remote repository into your local repo.

   Compared with git pull and git Fetch:
   same point is that available to accomplish the task.
   different point is that git fetch is much safer than git pull.

3.1: Works with remote branches

To gain a deeper understanding of how git fetch operates, it's helpful to explore the way Git manages and archives commits. Within a Git repository, there is a hidden directory named `.git/objects`. This directory serves as the storage for all commits, encompassing both those from local and remote sources. To differentiate between commits from local and remote branches, Git utilizes branch references (refs). The refs associated with local branches can be found in the `.git/refs/heads/` directory. When you run the git branch command, it displays a list of these local branch refs.


Examples in two ways:
1. way one: 
   ```
   git branch # typed by user
   main
   CSC207
   CSC301
   CSC209

   ```

   
2. way two:
   ```
   /.git/refs/heads/ # typed by user
   main
   CSC207
   CSC301
   CSC209

   ```

    
Remote branches function similarly to local branches, but they correspond to commits in another user's repository. To avoid confusion with local branches, remote branches are identified with a prefix indicating the remote repository they belong to. Similar to local branches, Git maintains reference pointers (refs) for these remote branches as well. These refs for remote branches are stored in the `.git/refs/remotes/` directory. In the following example, you'll see the branches that might appear after fetching from a remote repository, which we'll refer to as `remote-repo`:

   ```
   git branch -r # typed by user
   origin/main
   origin/CSC301
   origin/CSC207
   remote-repo/main
   remote-repo/other-file
   ```

The output shown includes the local branches previously mentioned, but now they are prefixed with `origin/`. It also lists the remote branches, prefixed with remote-repo. Checking out a remote branch is similar to checking out a local branch, but it results in a detached HEAD state, akin to checking out an older commit. These remote branches can be considered as read-only. To see your remote branches, you can use the `git branch` command with the `-r` flag.

3.2: More options? 

`git fetch <remote>` 

Fetch all of the branches from the repository.
Downloads all of the required commits and files from the other repository.

`git fetch <remote> <CSC301>`

Only fetch the specified branch. In this example, fetch the branch named by CSC301.

`git fetch --all`

A powerful command that retrieves all branches from every registered remote repository.

