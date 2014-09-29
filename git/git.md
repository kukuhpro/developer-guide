# Git Workflow Guideline

This document explains about using Git workflow on development with team. Please make sure you're using Git 1.7.2 or above.

## Branches

- **master**: main branch which reflect the live version
- **develop**: active branch for daily development
- **feature**: checkout this branch from `develop` to start developing new feature
- **hotfix**: checkout this branch from `master` to fix issues and merge back to both `master` and `develop` after done with the development on this branch.

## Lifecycle

Bearing in mind that you will always being doing your work and commits locally, a typical session looks like this:

```
git clone git@bitbucket.org:xmgravity/xmproject.git
```
Get a copy of the central storage facility (the repository).

```
git checkout develop
```
Switch to branch **develop** to start on development. 

```
git checkout -b feature/new-feature-1
```
Create a local branch called "feature/new-feature-1" to start developing on new feature.

Now, start creating, editing files, testing. When you're ready to commit your changes:

```
git add [file]
```
This tells git that the file(s) should be added to the next commit. You'll need to do this on files you modify, also.

```
git commit -m "[commit message]"
```
Commit your changes locally.

And finally:

```
git push origin feature/new-feature-1
```
This command pushes the current state of your local repository, including all commits, up to remote repository. Your work becomes part of the history of the `feature/new-feature-1` branch on remote repository.

`git push` is the command that changes the state of the remote code branch. Nothing you do locally will have any affect outside your workstation until you push your changes.

`git pull` is the command that brings your current local branch up-to-date with the state of the remote branch on github. Use this command when you want to make sure your local branch is all caught up with changes push'ed to the remote branch.

Once you're done developing this feature, create a pull request from `feature/new-feature-1` to `develop`. 

### Some useful terms

**master**: this is the main code branch, equivalent to trunk in Subversion. Branches are generally created off of master.

**origin**: the default remote repository that all your branches are pull'ed from and push'ed to. This is defined when you execute the initial git clone command.

**unpublished vs. published branches**: an unpublished branch is a branch that only exists on your local workstation, in your local repository. Nobody but you know that branch exists. A published branch is one that has been push'ed up to github, and is available for other developers to checkout and work on.

**fast-forward**: the process of bringing a branch up-to-date with another branch, by fast-forwarding the commits in one branch onto the other.

**rebase**: the process by which you cut off the changes made in your local branch, and graft them onto the end of another branch.

## Line endings

All text files in must be normalized so that lines terminate in the unix style (LF).  In the past, we have had a mixture of termination styles.  Shortly after the migration to Git the master and maintenance branches were normalized to LF.  Please do not commit files that terminate in CRLF!

### Configuring git to enforce LF normalization

There are several way to enforce LF normalization. Each method carries some consequences, and the consequences & methods differ between versions of Git.

#### `autocrlf` property

Normalization rules for all text files can be addressed by the 'autocrlf' configuration property. There are two useful values for this property, depending on your platform

- autocrlf = input. Use on unix-like platforms. This will perform no conversion upon checkout, but will normalize any crlf files upon commit.

- autocrlf = true. Useful on Windows platforms. This will have the effect of converting all text files into dos-style (CRLF) in the working copy upon checkout. Upon commit, all files will be normalized to LF on their way into the repository, but remain in CRLF in the local working copy directory.

This property can be set globally for all local git repositories, or locally for a single git repository.

The `autocrlf` property can be set globally via the command line. For example:

```
git config --global core.autocrlf input
```

Executing this command is identical to editing your `~/.gitconfig` file and adding:

```
[core]
        autocrlf=input
```

The `autocrlf` property can also be set locally for a given git repository, such as the local clone of the fcrepo. For example, from within the local working directory:

```
git config core.autocrlf input
```

Executing this command is identical to editing the `.git/config` file within the git working directory and adding:
```
[core]
        autocrlf=input
```

##### .gitattributes file

The presence of a committed .gitattributes file within the code can also be used to apply line-ending rules. This has the benefit of being part of the managed sources (and this part of a given branch, tag, etc), but is not understood by all versions of git. The fedora master branch has a .gitattributes file containing * text=auto, which instructs git to detect text files, and normalize to LF at each commit.

## Commit Message

- First line: brief description (~ 50 characters)
- Second line: blank
- Following lines: more detailed description, line-wrapped at 72 characters. May contain multiple paragraphs, separated by blank lines. 

Use the present tense when writing messages, i.e. "Fix bug, apply patch", not "Fixed bug, applied patch."

#### Sample

```
Create .gitattributes file to normalize line feeds

Create .gitattributes file requesting all text files normalised to LF.
Will be ignored by git versions < 1.7.2

See https://wiki.duraspace.org/display/FCREPO/Git+Guidelines+and+Best+Practices
for more information.
```

## Pulling and pushing to master
All `pull` or `merge` operations from remote/master into the local master branch should be fast-forward. Do not perform development in the master branch, periodically update with `pull`, and then `push` your local master. Instead, perform local commits in a separate branch, and merge (or rebase and merge) with master right before pushing it.

`git pull -ff-only` can be used to assure that a pull is fast-forward only. If a fast-forward pull is not possible, this flag will cause git to exit with an error, and leave the local branch untouched.

### Development directly in master

This should be avoided for all but the simplest commits that are immediately pushed. If you have several un-pushed commits, and then use git pull to merge in remote changes, that pull will be non-fast-forward. In other words, git pull will automatically create a merge commit which merges origin/master into your local branch. A subsequent push will publish your local master to the central repository, and the presence of the merge commit with origin/master might make a confusing-looking history.

### Development in a local branch

Development in a local branch (even with occasional merges with master) is a valid and recommended development pattern. If parallel commits have been pushed to master in the meantime, this workflow will represent your local changes as if it indeed were a separate branch.

