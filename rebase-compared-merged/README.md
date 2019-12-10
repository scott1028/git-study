# How to reduce those differences?

- `BACKUP` branch: original `master` branch backup.
- `BACKUP#FEATURE`: original `feature` branch backup.

- By `rebase` way, if there are lots conflict `commit`, it will cause multiple manual confict resolutions.

```
git checkout feature
git rebase master
```

- By `merge` way, if there are logs conflict `commit`, it only casue one manual conflict resolution.

```
git checkout feature
git merge master
```

