# Spliting repos appart

1. Clone original repo
1. Remove original origin
1. Filter out the rest using *--subdirectory-filter* (or any other directive)
1. Clean out the original refs
1. Make new origin repo 
1. Push


Filter recipe example:
```
git filter-branch --subdirectory-filter vim -- master
git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin
git reflog expire --expire=now --all
git gc --prune=now
git remote add origin git@github.com:sthysel/dotvim.git
```
