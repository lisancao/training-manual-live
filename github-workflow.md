# Git Workflow

The following is a recommended git workflow for developing notebooks. Its main goals are to encourage regular commits of notebook code and to provide release coordinators with flexibility when preparing to merge content into the master branch.

## Levels

There two types of branches:

1. master
2. individual notebooks or stories

Most developers will do work solely within individual branches, making sure to occasionally fetch and merge changes from the master branch.

In a usual software development project, the second level would more commonly be referred to as *feature branches*. In this project, individual notebooks take the place of individual features.

## Working on a Branch

Keeping to a single notebook per *feature branch* gives release coordinators the flexibility to grab notebooks that are ready and leave those that are not when it comes time to prepare for a release.

More than one developer can work on the same notebook branch, and you shouldn't be terribly concerned with checking in polished work at this level, except to the extent that it may disrupt anyone else working with you on the same notebook. A little communication goes a long way here. That said, we expect that it will largely be a single developer working on a particular notebook at a time.

Get comfortable with making regular, small commits to your notebook branch, and push to GitHub fairly often. This makes merging easier down the line, makes it easier for other developers to review progress, and ensures that your work is backed up.

Occasionally developers working on the individual notebook branches will want to do the following:

```bash
git fetch
git merge master
```

to make sure they’re up to date with the upstream changes and are always ready to be merged into *master*. This will become more important the closer those individual notebook branches get to being integrated into *master*.

Notebooks will undergo reviews before being added to master.

## Master Branch

This represents "releasable" code. In theory, anyone checking out code from the *master* branch should expect to see the best quality notebook code that we can offer. It won’t necessarily be bug free, but it's free of the bugs we know about (and that are serious enough to block a release).

## Commit Messages

Capitalize the first letter, no period. Use the imperative "Fix bug" not "Fixes bug" or "Fixed bug". 
Include the Jira task identifier in the commit message (not in the file title), for example: "CC-33 Add interactivity to the plots". For longer commit message write a short description followed by a blank line and then the longer description. Try to wrap at 72 characters, in Vim this is done with ```:set textwidth=72```. Use the body to explain what and why but not how.

## Tagging

It’s often helpful to mark a specific commit of the master branch when that commit represents code we know has been "released" and will likely not be continually updated from Github until the next release. This can come in handy when tracking down bug reports that may or may not have been fixed since that release.

Individual developers working on notebook branches do not have to worry about tagging, but in the event that a release coordinator wants to tag a release, they can run the following:

```bash
git tag -a v1.0 -m "our first release"
```

## Common Commands

Here are some of the common commands that developers will be using:

### Committing and Pushing Code:

```bash
git add some_file
git add some_other_files*
git status
git commit
git push
```

### Create a Branch

This will create a branch locally and remotely, based off of *master*:

```bash
git checkout master # if not already there
git checkout -b branch_name
git push -u origin branch_name
```

### Merge Master into a Branch

```bash
# Fetch the remote branch and merge it into the local branch
git pull
git checkout branch_name # if not already there
git merge master
```

### Compare Changes to Committed Work:

```bash
git diff
```

### Compare Differences Between Branches:

```bash
git diff staging notebook_a
```

Compare with upstream changes on the same branch and then merge (more complicated than git pull, but also avoids potential surprise merge conflicts):

```bash
git fetch
git checkout branch_name
git diff origin/branch_name
# assuming the changes are okay...
git merge origin/branch_name
```

### Temporarily Stash Local Changes:

```bash
git stash
```

The moves local changes out of the way, making your repository look clean. It can be useful when you realize there are upstream changes but don't want to commit your current changes just to see those upstream changes.

When ready, you can then reapply your local changes via:

```bash
git stash pop
```
