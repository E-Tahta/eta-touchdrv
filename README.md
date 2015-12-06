# ETA-TOUCHDRV

**NOTE:** Following git and gbp commands are not fully tested yet.

## Introduction

eta-touchdrv project provides kernel modules and their corresponding daemons for
non-hid 2-camera and 4-camera touchscreen sensors of Fatih Interactive White
Boards. Kernel modules are open-source, but source code of server daemons are
unavailable. They are provided by Vestel.

## Maintenance

Create topic branches (i.e. topic/bugfix, topic/new-feature) off the master.

```bash
git checkout -b topic/bugfix master
# hack hack hack to fix the bug
```

Impelement the feature or fix the bug and merge it back to master if it passes
all the tests.

```bash
git checkout master
git pull
git checkout topic/bugfix
git rebase master
git checkout master
git merge topic/bugfix --no-ff
```

## Packaging

For debian packaging we have debian/sid branch in our repo. You can also create
your packaging branches like debian/experimental. Create ChangeLog for master
and tag it with the pattern `vx.y.z` and merge the tag into debian/sid
branch. Edit debian/changelog and build debian package. Before a release package
you might want to build several experimental snatshot packages.

Here is how you could get a snotshot build.

```bash
git checkout master
git pull
# Hack master
git commit -am "Add new hacks"
git log master --pretty --numstat --summary --no-merges | git2cl > ChangeLog
git add ChangeLog
git commit -m "Update ChangeLog"
git checkout -b debian/experimental debian/sid
# edit debian/gbp.conf for experimental builds
# debian-branch = debian/experimental
# upstream-tree = branch
git commit -am "Experimental builds"
git merge master
gbp dch --snapshot --auto debian/
gbp buildpackage --git-ignore-new -uc -us
```

When you are sure it is time to have a release build,

```bash
git checkout master
git tag vx.y.z
git checkout debian/sid
git merge master
# You might want to hack some debian/* files.
# In case you had some changes
git commit -am "Add new changes to debian/*"

gbp dch --release --auto debian/
git commit -am "New release vx.y.z"
gbp buildpackage -uc -us --git-tag
```

This will be automatically tagged with debian/sid/x.y.z-d
