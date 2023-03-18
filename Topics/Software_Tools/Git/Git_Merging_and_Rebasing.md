# `git merge` vs. `git rebase`

Both `git merge` and `git rebase` are methods for integrating new commits that are on separate branches. However merging is usually what is taught in CSC207, and many students have never heard of rebasing, or have had very little experience with it. Here are some resources to get you started with learning about rebasing and the difference between the two commands!
1. [Git Basics: Merge and Rebase](https://www.youtube.com/watch?v=dO9BtPDIHJ8&ab_channel=EnvatoTuts%2B) (YouTube video) 
    
    This is a very short introduction on merge vs rebase. It goes over the most basic differences between them and provides a short example of a workflow that uses merge and a workflow that uses rebase. This is a good starting point, but you will likely need to visit the below resources as well to deepen your understanding. It can also be good video to return to if have learned this in the past and need to refresh your memory.

2. [Learn Git Rebase in 6 minutes // explained with live animations!](https://www.youtube.com/watch?v=f1wnYdLEpgI&ab_channel=TheModernCoder) (YouTube video)
    
    This video also goes over the differences between merge and rebase, but it goes into much more depth than the previous video. In particular, it provides a  detailed demo of a workflow that uses `git rebase` that models real world scenarios well. If you would like to try implementing rebasing in your workflow, the Demo section of this video will be helpful for that.

3. [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) (Atlassian article)
    
    If you prefer to read an article over watching a video, this is the resource for you, as it covers all of the topics that the above two videos cover. It also covers more scenarios that you may find yourself in while using rebase as part of your workflow. In particular, the section called [The Golden Rule of Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) will help you make sure that you don't accidentally bring catastrophe upon your repository while using rebase. Additionally, there is a short section on interactive rebase, a powerful tool that give you control over your branch history. 