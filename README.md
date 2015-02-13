# fc-submodule
Sandpit for working with submodules in a gitflow environment

# Adding cpp0x submodule
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
