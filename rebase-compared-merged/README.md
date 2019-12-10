# How to reduce those differences?

- `BACKUP` branch: original `master` branch backup.
- `BACKUP#FEATURE`: original `feature` branch backup.

- By `rebase` way, if there are lots conflict `commit`, it will cause multiple manual confict resolutions.

```
git checkout feature
git rebase master
```

###### Note: When you are use `rebase`, compared with same file of last commit, please don't let conflict file no any changes

- By `merge` way, if there are logs conflict `commit`, it only casue one manual conflict resolution.

```
git checkout feature
git merge master
```

# Where history of `rrr` stored?

```
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ git status
On branch feature
nothing to commit, working tree clean
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ git merge master 
Auto-merging index.js
CONFLICT (content): Merge conflict in index.js
Recorded preimage for 'index.js'
Automatic merge failed; fix conflicts and then commit the result.
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ vim index.js 
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ git add index.js 
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ git status
On branch feature
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   index.js

scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ git commit
Recorded resolution for 'index.js'.
[feature 59a3dda] Merge branch 'master' into feature
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ git status
On branch feature
nothing to commit, working tree clean
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ ls
index.js
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ ls .git/
branches/       COMMIT_EDITMSG  config          description     HEAD            hooks/          index           info/           logs/           MERGE_RR        objects/        ORIG_HEAD       refs/           rr-cache/
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ ls .git/r
refs/     rr-cache/ 
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ ls .git/rr-cache/
b25c5e3701a202557c4d7eaaad1c2552d0bb9a09
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ 
```
