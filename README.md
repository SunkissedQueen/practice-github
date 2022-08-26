[Undo Merge](https://www.datree.io/resources/git-undo-merge)

- commits are listed in older to current commit

If you were still in the merge process, you could run git merge --abort to cancel the merge - Git cleans up everything nicely and you’d end up in the state your main branch was in before.

However, if you’ve already finished your merge, there’s no such option. Instead, here’s what you’ll need to do: first, make sure you check out the main branch that you merged your changes into. You’ll want the next steps to affect this branch.

Next, find the commit hash of the merge with git log:

The commit hash is the seven character string in the beginning of each line. In this case, `52bc98d` is our merge’s hash. Once you have that, you can pass it to the git revert command to undo the merge:

The git revert command will have generated a commit that restores your branch’s state to where it was before the faulty merge. If your merge was remote (i.e. happened on GitHub) you can push this commit like any other and you’ll be set to go.

[More Undo commands](https://dev.to/zigrazor/git-undo-merge-the-final-guide-4bj9)

Git Undo Merge
To undo a git merge, you need to find the commit ID of your last commit. Then, you need to use the git reset command to reset your repository to its state in that commit. There is no “git revert merge” command.

The steps to revert a merge, in order, are:

git log OR git reflog (to find the last commit ID)
git reset –merge (to revert to the commit you specify)

Say we have accidentally merged two branches that should not be merged. We can undo these changes.

Undo Merge Git Example
Find the Commit ID
To start, we need to find out the commit ID of the commit before our merge on our remote repository. You can do this using git reflog:

This command tells us that the last commit has the hash a9fdeb5.

Alternatively, you can use the git log command. But, the reflog command returns an output that is easier to read. This is why we opted to use reflog instead of the log command.

Revert to the Commit
We can use this hash to revert the merge commit with the git reset –merge command:
git reset --merge a9fdeb5
This command resets our repository to the state it was at in the a9fdeb5 commit on the master branch.

The –merge flag resets an index and updates all the files that are different between the current state of your repository and the HEAD.

This flag does not reset files with changes that have not been added to a commit. This makes it safer than using the oft-recommended git reset –hard command.

Once we have reset our repository, we can make the relevant changes to our code. Then, we can push them to a remote branch using the git push command.

The HEAD Shorthand
The Git HEAD keyword refers to the latest commit in your repository. You can use the Git HEAD shorthand to undo a merge:
git reset --merge HEAD~1
This command reverts our repository to the last commit. HEAD refers to the current state of your repository; HEAD~1 is the last commit in your repository.

Additional Notes
If you need to push the branch to the remote, and you have already pushed the merge, you need to use:
git push -f origin myBranch 
to let Git force the push and overwrite the history of the branch.
PAY ATTENTION: this can be dangerous if myBranch was already fetched by others in their own repo.

Need to clean up these notes
