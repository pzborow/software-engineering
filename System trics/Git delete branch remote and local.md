# Git delete branch remote and local

## Executive Summary

```bash
$ git push -d <remote_name> <branchname>
$ git branch -d <branchname>
```

**Note:** In most cases, &lt;remote_name&gt; will be origin.

## Delete Local Branch

To delete the **local** branch use one of the following:

```bash
$ git branch -d <branch_name>
$ git branch -D <branch_name>
```

The -d option is an alias for --delete, which only deletes the branch if it has already been fully merged in its upstream branch.
The -D option is an alias for --delete --force, which deletes the branch "irrespective of its merged status." \[Source: man git-branch\]
You will receive an error if you try to delete the currently selected branch.
Delete Remote Branch
As of Git v1.7.0, you can delete a remote branch using

```bash
$ git push <remote_name> --delete <branch_name>
```

which might be easier to remember than

```bash
$ git push <remote_name> :<branch_name>
```