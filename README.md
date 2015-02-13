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

# How to develop in this repository
A gitflow workflow is used, so for the easiest integration you should
run

```
$ git flow init
```

after cloning. **NOTE**: because the upstream repo uses a gitflow layout,
you will be on the `develop` branch after a `git clone`. Ensure that
you use `master` for the production release branch when running `git flow init`.

# Adding the cpp0x submodule
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

