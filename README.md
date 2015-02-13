# fc-submodule
Sandpit for working with submodules in a gitflow environment

# How to clone this repository
This is a test of working with the `FNALCore` package using git submodules
to merge in the highly coupled subpackages `cpp0x`, `cetlib`, `fhicl-cpp`
and `messagefacility`. Because submodules are used, additional steps are
needed when cloning the repository:

```
$ git clone https://github.com/drbenmorgan/fc-submodule.git
...
$ cd fc-submodule
$ git submodule init
...
$ git submodule update
```

A simpler way is to use the `--recursive` option to `git clone`:

```
$ git clone --recursive https://github.com/drbenmorgan/fc-submodule.git
```

# How to update/monitor this repository
This assumes you are simply consuming the repository and are not bothered
about working with the submodules at all.

```
... Fetch and merge as normal ...
$ git fetch
$ git merge

... Superproject only updates commit pointed to in submodule, so also do ...
$ git submodule update
```

You can get the state of the submodule status at any point by running

```
$ git submodule status
 9a1254959c86bcd26ef5ce19d0b63aecc72a5fa6 FNALCore/cpp0x (v1_04_01-0-3-g9a12549)
```

This lists the commit at which the submodule is at, plus a description of
the commit (basically the same format as `git describe` outputs)


# How to develop in this repository
A gitflow workflow is used, so for the easiest integration you should
run

```
$ git flow init
```

after cloning. **NOTE**: because the upstream repo uses a gitflow layout,
you will be on the `develop` branch after a `git clone`. Ensure that
you use `master` for the production release branch when running `git flow init`.

# Adding/Updating the cpp0x submodule
```
... This will add the submodule at the tip of the default branch ...
$ git submodule add https://github.com/drbenmorgan/fnal-cpp0x-flow.git FNALCore/cpp0x
... Go into submodule, checkout a tag
$ cd FNALCore/cpp0x
$ git checkout v1_04_01-0
... Go back to base repo, add, and commit
$ git add FNALCore/cpp0x
$ git commit
```

The steps of checking out a tag and commiting are all that's needed if
you want to maintain the superproject but not the submodule (directly).


# Working with the cpp0x submodule directly
If you have push permissions to the upstream repo for a submodule, you
can make local commits and push them to the upstream. The best way to do
this is:

- (Optional) create a feature branch of the superproject
- create a feature branch in the submodule
- make the needed commits
- push these to the parent repo of the submodule
- add the changed submodule in the superproject, make a superproject
  commit
- (If superproject feature branch created) Finish superproject feature

FNALCore submodules should use a gitflow branching structure, so patches
should be applied on a feature branch off of `develop`. The steps to do
this, using `cpp0x` as an example, are thus:

```
$ cd FNALCore/cpp0x
$ git checkout develop
$ git fetch
$ git merge

... If not already done so, create the git flow structure (as above, ensure master branch is used for releases! ...
$ git flow init

... Create a feature branch for patches ...
$ git flow feature start fnalcore-patches

... make changes, commit, and publish feature to submodule parent ...
$ git commit -m "Final changes to update cpp0x"
$ git flow feature publish
```

One could at this point also finish the feature and go through the gitflow
release process in the submodule, before finally checking out the new
release tag in the submodule. In either case, we end up with the submodule
at a new commit which is also published in the upstream repo.

Just as before, to update the superproject to use the submodule at this
commit, we go back to the root directory of the superproject and do

```
$ cd ../..
$ git add FNALCore/cpp0x
$ git commit -m "Patched cpp0x"
$ git push origin
```


