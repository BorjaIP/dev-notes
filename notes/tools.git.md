---
id: 2r0idv7bwuzar0btpe5tnsd
title: Git
desc: ''
updated: 1680196998250
created: 1680196301498
---

## Remove large files from history

Tool [bfg](https://github.com/rtyley/bfg-repo-cleaner) for use with large files.

```bash
# Find the largest files in .git:
git rev-list --objects --all | grep -f <(git verify-pack -v  .git/objects/pack/*.idx| sort -k 3 -n | cut -f 1 -d " " | tail -10)
# To remove all blobs from history, whose size is superior to 100Mb
# Execute the previous command for see the results
bfg -b 100M
# Execute this commands below for erase commits and old files
git reflog expire --expire=now --all
git gc --prune=now --aggressive
# Push changes
git push origin <your_branch_name> --force
```
