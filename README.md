# redo

A planned C implementation of D. J. Bernstein's `redo`, extended with support
for environment variable and non-project file dependencies.  Supporting
multi-output rules would be nice too.

## Planned extensions

* Dependencies on environment variables and non-project files (such as the C
  compiler)
  - With symlink special-casing
    - default: track dereferenced file
    - no-follow: track the symlink itself
* Multi-output rules (like with LaTeX)
  - Maybe `.do` files can specify *additional* outputs?
  - With `redo-addtarget`
  - After a cold run, the central database can keep track of it?
  - Benefits: compatible with other `redo` implementations (other than the new
    command)
  - Consequences: a "main" target has to be decided beforehand
* Directory dependencies?  (I'm not sure how useful this is)

## Goals

* (For the author:) Be good practice for writing non-trivial C programs
* Be fast and run rules in parallel
* Avoid unintuitive or untransparent behaviour
* Support non-sh (including binary) `.do` files (just be executable!)

## Implementation notes

* Store hashes of dependencies to check for new-ness
* Use SQLite for a small and fast database library
  - Store project files, non-project files, and environment variable hashes in
    separate SQLite databases?  To maximise concurrent reads/writes, since the
    rate of change of each type differs from each other

## Other implementations

* [apenwarr/redo](https://github.com/apenwarr/redo/)
