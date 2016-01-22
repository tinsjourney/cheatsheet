# Delete branches / tags

localy
 git branch -d <branch_name>
 git tag -d <tag_name>

remotely
 git push origin :<branch_name>
 git push origin :<tag_name>

This won't work if you have a tag with the same name as the branch on the remote:

 $ git push origin :branch-or-tag-name
 error: dst refspec branch-or-tag-name matches more than one.
 error: failed to push some refs to 'git@github.com:SomeName/some-repo.git'

In that case you need to specify that you want to delete the branch, not the tag:

 git push origin :refs/heads/branch-or-tag-name

Similarly, to delete the tag instead of the branch you would use:

 git push origin :refs/tags/branch-or-tag-name

# Closing github issues with commit
 git commit -m "Fixes/Closes/Resolves #<issue_number>"

# Merge two Git repositories without breaking file history
1. Add the second repo as a remote :
```
cd firstgitrepo
git remote add secondrepo username@servername:andsoon
```
2. Make sure that you've downloaded all of the secondrepo's commits:
```
git fetch secondrepo
```
3. Create a local branch from the second repo's branch:
```
git branch branchfromsecondrepo secondrepo/master
```
4. Move all its files into a subdirectory:
```
git checkout branchfromsecondrepo
mkdir subdir/
git ls-tree -z --name-only HEAD | xargs -0 -I {} git mv {} subdir/
git commit -m "Moved files to subdir/"
```
5. Merge the second branch into the first repo's master branch:
```
git checkout master
git merge branchfromsecondrepo
```
Your repository will have more than one root commit, but that shouldn't pose a problem.
