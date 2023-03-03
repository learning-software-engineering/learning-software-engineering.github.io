## Resources for Development Process

### Git Flow:
#### Git Branching
* [Learn Git Branching](https://learngitbranching.js.org/)
  * **Learn Git Branching** is an interactive websites that teaches git branching concepts/commands through visualization. The website cover local and remote Git concepts, including cherry-picking, rebasing, fetching, pushing etc. Learn Git Branching is a great resource for anyone looking to learn Git and improve their Git skills.
  * Feel free to checkout their GitHub: [Learn Git Branching GitHub](https://github.com/pcottle/learnGitBranching), as they have provided some website instruction including levels and sandbox mode. You can also contribute to it if you are interested.
* Main
  * ```git commits -m "[MESSAGE]"```
     * Records a snapshot of the state of the repository
     * When commit is made, you stage the changes and then commit them
     * The command create a new commit that includes the changes you have made, along with a messages that describe the changes
     * Maintain a history of commits that were made (Use ```git log``` to see full commit history)
  * ```git branch [BRANCH NAME]```
     * Pointers to specific commit
     * Developer can work on a specific feature or bug fix on a branch before merging with the main branch
  * ```git checkout [BRANCH NAME]```
     * Move to [BRANCH NAME] 
     * ```git checkout -b [BRANCH NAME]```: Create a new branch and check it out at the same time 
  * ```git merge [BRANCH NAME]```
     * Combining branches into a single branch
     * Merging the current branch with [BRANCH NAME]
     * Three possible outcomes, including fast forward merge, recursive merge, merge conflict
  * ```git rebase [BRANCH NAME]```
     * Another way to combine work between branches
     * Move the entire branch to [BRANCH NAME], apply changes on the current branch to [BRANCH NAME]
     * Produce a linear sequence of commit, commit history will be cleaner

* Remote
  * ```git fetch```
     * Download commits from remote that are missing in local repository
     * Note that it does not change any of your local files
  * ```git pull```
     * fetching remote changes and merging it to the current state



