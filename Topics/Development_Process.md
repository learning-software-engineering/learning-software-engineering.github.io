## Resources for Development Process
1. GitFlow
    1. Stash
        git stash
            saves a change before switching to a new branch
        git stash pop
            applies the latest stash and deletes the stash from the stash list
        git stash list
            shows the list of all stashes
        git stash apply stash_ID
            apply the # or stash ID from the stash list
        git stash drop stash_ID
            deletes the stash with stash_ID from the stash list
        git stash clear
            deletes all stash
    2. Retrieve Lost Commits
        gitk --all $(git fsck --no-reflog | Select-String "(dangling commit )(.*)" | %{ $.Line.Split(' ')[2] })
        git apply ##### 
            OR 
        Search inside the pop up window and simply copy paste the code back
        Link: https://stackoverflow.com/questions/89332/how-do-i-recover-a-dropped-stash-in-git
    3. Revert Single File From Commit
        git checkout [commit ID] -- path/to/file
        Link: https://dev.to/lofiandcode/git-and-github-how-to-revert-a-single-file-dha
    4. Revert Multiple File From Commit
        git reset --soft HEAD^
        git restore --staged path/to/unwanted_file
        #Note: NEVER remove the "--soft" tag, because if you remove it. The reset will be a hard reset and will remove all the changed files from the commit and sometimes it will lead into lost files and you will need to go back to "1. Retrieve Lost Commits". So for a safe practice, just use the soft reset ("--soft")
        Link: https://stackoverflow.com/questions/12481639/remove-file-from-latest-commit

4. Pull-requests
    1. Update Pull-requests
        After pushing your commits to create a new pull request, sometimes you realize you need to change a file that is already committed on the pull request. So you would change the file, git add, commit, push it and then realize you cannot push it. The following command will help you resolve this issue.

        git push origin master --force

        #Note: Use with precaution because we are using the force push. So try to limit the usage of this to directly push codes to the master branch. A great alternative would be using --force-with-lease because it does not overwrite any work on the master branch if more commits are added to the master branch. (In depth comparisons of force vs force-with-lease https://itnext.io/git-force-vs-force-with-lease-9d0e753e8c41)