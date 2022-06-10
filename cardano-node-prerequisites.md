---
description: >-
  Now the most complicated part (not so complicated if you follow this guide :)
  ) - the installation process!
---

# Getting ready to install the Cardano Node (v1.34.1)

to successfully install (compile) the Carano node, we need to be sure that we have all the necessary ingredients! To get them (install) type the following commands:

```
sudo apt-get update -y
sudo apt-get upgrade -y
```

```
sudo apt-get install curl wget python3 build-essential pkg-config libffi-dev libgmp-dev libssl-dev libtinfo-dev systemd libsystemd-dev libsodium-dev zlib1g-dev yarn make g++ jq libncursesw5 libtool autoconf automake git tmux htop nload -y
export LD_LIBRARY_PATH="/usr/local/lib:$LD_LIBRARY_PATH"
```

This will install all the necessary software packages for our next steps.

As the Cardano node is using **cabal**, so let's install it as well. We will use the recommended version 3.4.0.0 and install it to our local bin folder (_.local/bin_)

to install cabal, we will be using **ghcup** (_ghcup_ is an installer for\
the general-purpose language [Haskell](https://www.haskell.org/)), more info you can check: [https://www.haskell.org/ghcup/](https://www.haskell.org/ghcup/)&#x20;

```bash
curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh
```

This Haskell installation script will ask for input:

![Haskell Installation script](<.gitbook/assets/CleanShot 2021-08-30 at 13.08.19.png>)

Press **ENTER** to continue

* When asked _**"Do you want ghcup to automatically add the required PATH variable to "/home/cardano/.bashrc?"**_  **press "A"**
* When asked _**"Do you want to install haskell-language-server (HLS)?"**_ Answer "No" (**by pressing "N"**)
* When asked  _**"Do you want to install stack?"**_ Answer "No" (**by pressing "N"**)

![](<.gitbook/assets/CleanShot 2021-08-30 at 13.15.55.png>)

**Press ENTER** to proceed with cabal installation

When the installation is finished, you should see the following screen:

![](<.gitbook/assets/CleanShot 2021-08-30 at 13.18.58.png>)

let's reload environment variables:&#x20;

```
source /home/cardano/.ghcup/env
```

Let's install the 3.4.0.0 version and set this one as the default:

```
ghcup install cabal 3.4.0.0
ghcup set cabal 3.4.0.0
```

Let's check which version we have installed

```
 cabal --version 
```

you should see version 3.4.0.0

![](<.gitbook/assets/CleanShot 2021-08-30 at 13.23.56.png>)

&#x20;You should now have the cabal installed in _/home/cardano/.ghcup/bin_ folder.

### GHC 8.10.4 installation

Let's move to the next steps - installing GHC - the Haskell code compiler (Cardano node is based on the Haskell programming language).&#x20;

As we already installed the handy ghcup tool, then this is done super easy:&#x20;

```
ghcup install ghc 8.10.4
```

![GHC installation](<.gitbook/assets/CleanShot 2021-08-30 at 13.30.44.png>)

After a short while, you should have GHC installed!\
Let's set it as the default version:

```
ghcup set ghc 8.10.4
```

And check if everything has gone as planned:

```
ghc --version
```

You should see:

![GHC version check](<.gitbook/assets/CleanShot 2021-08-30 at 13.33.23.png>)

### Install Libsodium

One more thing we need is the Libsodium libraries so let's do this! \
let's create a git folder where we will be compiling libsodium library from the source code:

```
mkdir -p ~/git && cd ~/git
```

Download and install libsodium library ( we need a specific branch of the library, so follow the guide)

```
git clone https://github.com/input-output-hk/libsodium
cd libsodium
git checkout 66f017f1
./autogen.sh
./configure
make
sudo make install

```

Let's add the following PATHs to our .bashrc file and load them.

```
echo "export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH" >> ~/.bashrc
echo "export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH" >> ~/.bashrc
source ~/.bashrc
```



Let's move to the next step - the actual installation of Cardano Node!
