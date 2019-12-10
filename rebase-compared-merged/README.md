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

- A resolution recorded in `.git/rr-cache` folder and it will be used when we encounter same situation like `preimage`.

###### `preimage`: conflict situation you encounter, `postimage` resolution you should use.

```
scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ cat .git/rr-cache/b25c5e3701a202557c4d7eaaad1c2552d0bb9a09/preimage 
'use strict';

const main = () => {
<<<<<<<
=======
    console.log('History#1', 'History#2.5', 'History#3');
>>>>>>>
};

scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ cat .git/rr-cache/b25c5e3701a202557c4d7eaaad1c2552d0bb9a09/postimage 
'use strict';

const main = () => {
    console.log('History#1', 'History#2.5', 'History#3', 'Should be deleted');
};

scott@scott-mint:~/workspace/git-study/rebase-compared-merged/git-rerere$ 
```

# `Rerere` in `.gitconfig`

```
[rerere]
        enabled = true
```

####### Reference: https://medium.com/@kmsh3ng/%E4%BD%BF%E7%94%A8-git-rerere-%E8%87%AA%E5%8B%95%E8%A7%A3%E9%99%A4%E5%90%8C%E9%A1%9E%E5%9E%8B%E7%9A%84%E8%A1%9D%E7%AA%81-1f60748ce55b
