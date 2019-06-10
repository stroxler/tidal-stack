# tidal-stack

A stack-friendly wrapper for tidal.

The main methods for installing tidal assume a global install for ghc and thus a globally available Tidal package.  This project provides a wrapper for Tidal adopting the usual stack conventions and localised project.

The project contains a relatively current stack.yaml, and pins the tidal version to a specific commit.

Usage
===

command line
---

```
git clone https://github.com/tonyday567/tidal-boot
cd tidal-boot
stack build
stack ghci --ghci-options -XOverloadedStrings
```

From this point, for testing, I usually cut-n-paste BootTidal.hs into ghci.

Note that the stack.yaml is using nightly-2018-12-01 which is ghc-8.6.2.  To pop back a version, to ghc-8.4.4, just use:

```
stack build --resolver=lts-12.20
```

installing and starting supercollider (on mac)
----------------------------------------------
You can generally `brew cask install supercollider`, or download and
install the app. You'll find the language interpreter inside the app.

To boot it up, I run
```
/Applications/SuperCollider.app/Contents/MacOS/sclang
  include("SuperDirt")
  SuperDirt.start
  s.options.device = "External Headphones"
```

using atom
----------
Run `stack exec atom` to start atom with the right ghc in the environment
vars. You'll want to install the `tidalcycles` plugin.

Note that if this repo has gotten stale, you may have problems; it's likely
that the atom plugin is expecting a newer version of tidalcycles. You can
probably just bump tidalcycles in `stack.yaml` to the latest release;
alternatively you could pin the plugin version; I had to update this
repo (which is forked from a December 2018 repo) to get it running
with the 3.0.0 version of the atom plugin.
emacs
---

emacs setup needs a slight tweak to use stack rather than cabal:

```
(require 'tidal)
(setq tidal-interpreter "stack")
(setq tidal-interpreter-arguments (list "ghci" "--ghci-options" "-XOverloadedStrings")
```

To test, open examples.tidal and run tidal-start-haskell <C-c C-s> and tidal-run-multiple-lines <C-return>.

