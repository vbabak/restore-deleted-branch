# restore-deleted-branch
How to deal with outdated and not supported branches and restore deleted branch on the Github.

## What are the restore options when deleting a branch?

### Branch was removed locally and remotely

```text
git push -d <remote_name> <branch_name>
git branch -d <branch_name>
```

After deleting branch locally and remotely (assume in all repository copies), 
the only way to restore branch is to checkout by commit hash of the branches (head) top commit. 
Commit hash is also known as 'sha'.

If you don't know the commit hash, you can find it with 
running

```text
git reflog
```

To restore the branch

```text
git checkout -b <branch> <hash>
```

### Branch was deleted after merging pull request on Github

This is the most straightforward way.
1. Create a branch. 
2. Commit and push changes.
3. Create pull request, merge it and delete the branch.

Because you have merged the code, more likely you will not need to restore the branch.
In case you need to recover deleted branch, you may do it easily from the "pull request" page.

### Branch was deleted after canceling pull request on Github

This is how I recommend to get rid of all non-fresh/non-supported branches. 
It could be POC (proof of concept) features branches, that was intensely developed in the past or 
parallel or alternative versions of the features. In this case you apparently don't
want to loose the code. And the list of such branches keep growing.

Is it possible to delete such branch with an option to restore it at any time? Yes! 
And here is how you can do that. 
1. Create a pull request but don't merge it. 
2. Name your pull request exactly the same as your source branch. 
- It does not matter if there will be a merge conflict, don't resolve it. 
3. Cancel this pull request.
4. Delete the branch.

Whether you need this branch in the feature or not, you will simply find it on the 
"Pull requests" page by the filter:

```text
head:your_branch_name
```

Open the pull request and press "Restore branch" button.

Related article [about stale branches](https://medium.com/@vbabak/how-to-deal-with-stale-branches-on-the-github-b49727480872)