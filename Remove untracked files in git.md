---
date: 2021-08-03
title: Remove untracked files in git 
slug: /coding/git/removing-untracked-files
aliases: []
---

In order to remove all files that are currently not under version control by Git from your current working directory, first perform a **dry-run**:

```bash
$ git clean -n -d 
Would remove subdir/a-file.md
Would remove another-file.md
```

If you're sure this is the desired result, delete the files for real:

```bash
$ git clean -f -d
Removing subdir/a-file.md
Removing another-file.md
```