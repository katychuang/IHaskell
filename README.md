This fork is my version of iHaskell with Plots for GHC 8.0 to generate charts. An example of a notebook is [here](https://github.com/katychuang/jupyter-notebooks/blob/master/facebook_posting_activity_haskell.ipynb).

Plots depends on Lens and Diagrams, so those libraries are supported also.

---

Credits:

![jupyter](https://i.imgur.com/S16l2Hw.png) ![IHaskell](https://i.imgur.com/qhXXFbA.png) [![Build Status](https://travis-ci.org/gibiansky/IHaskell.svg?branch=master)](https://travis-ci.org/gibiansky/IHaskell)


**IHaskell** is a kernel for the [Jupyter project](http://ipython.org), which allows you to use Haskell inside Jupyter frontends (including the console and notebook).


# Installation

## Linux

Some prerequisites; adapt to your distribution.

```bash
sudo apt-get install -y python3-pip git libtinfo-dev libzmq3-dev libcairo2-dev libpango1.0-dev
```

```bash
pip3 install -r requirements.txt
curl -sSL https://get.haskellstack.org/ | sh
git clone https://github.com/abarbu/IHaskell
cd IHaskell
stack install gtk2hs-buildtools
stack install --fast
stack exec ihaskell -- install
```

## Mac

These haven't been tested and there may be some missing required packages. But
they will be soon.

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install python3
brew install zeromq
curl -sSL https://get.haskellstack.org/ | sh
git clone https://github.com/abarbu/IHaskell
cd IHaskell
stack install gtk2hs-buildtools
stack install --fast
stack exec ihaskell -- install
```

# Running

```bash
stack exec jupyter -- notebook
```

## Where are my packages?

Stack manages separate environments for every package. By default your notebooks
will only have access to a few packages that happen to be required for
ihaskell. To make packages available add them to the stack.yaml in the ihaskell
directory and run `stack solver && stack install`.

Packages should be added to the `packages:` section and can take the following
form
([reproduced here from the stack documentation](https://github.com/commercialhaskell/stack/blob/master/doc/yaml_configuration.md#packages)). If
you've already installed a package by `stack install` you can simply list its
name even if it's local.

```
- package-name
- location: .
- location: dir1/dir2
- location: https://example.com/foo/bar/baz-0.0.2.tar.gz
- location: http://github.com/yesodweb/wai/archive/2f8a8e1b771829f4a8a77c0111352ce45a14c30f.zip
- location:
    git: git@github.com:commercialhaskell/stack.git
    commit: 6a86ee32e5b869a877151f74064572225e1a0398
- location:
    hg: https://example.com/hg/repo
    commit: da39a3ee5e6b4b0d3255bfef95601890afd80709
```
