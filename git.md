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
