---
description: Quick update guide from 1.33.0 (or older) to 1.34.1
cover: >-
  https://images.unsplash.com/photo-1558494949-ef010cbdcc31?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxfHxzZXJ2ZXJ8ZW58MHx8fHwxNjQ2MTM5ODI1&ixlib=rb-1.2.1&q=85
coverY: 0
---

# Upgrade to 1.34.1 from 1.3x.x

{% hint style="info" %}
if you are upgrading from older versions (1.29.0 or older) this upgrade will resync/replay all the blocks, so be ready that after the upgrade the node, depending on your server specs, will take some (30min - 2h) time to start.
{% endhint %}

Quick update guide for SPOs who have the previous version already installed  1.30.x\
If you are  installing from scratch, then follow the installation guide: [https://cardano-node-installation.stakepool247.eu/](https://cardano-node-installation.stakepool247.eu/)

1. Let's start with backing up current binaries

```
cd ~/.local/bin/

# let's create a folder with the version number
mkdir -p $(cardano-node version | grep -oP '(?<=cardano-node )[0-9\.]+')

# copying files to the created folder
cp cardano-node $(cardano-node version | grep -oP '(?<=cardano-node )[0-9\.]+')/
cp cardano-cli $(cardano-node version | grep -oP '(?<=cardano-node )[0-9\.]+')/
```

2\. Let's move forward with upgrading the system packages

```
# let's update the system first
sudo bash -c 'sudo apt-get update -y; sudo apt-get upgrade -y'
```

3\. let's download&#x20;

```
# let's create a directory where we will be downloading source code
cd ~
mkdir -p git
cd git
```

```
# just in case you already had a source directory with cardano-node source code - let's delete it and download fresh one.
rm -rf cardano-node
```

```
# let's clone source code from git
git clone https://github.com/input-output-hk/cardano-node.git

cd cardano-node
git fetch --all --recurse-submodules --tags

# checking out the 1.34.1 version
git checkout tags/1.34.1

```

```
# ensuring that we are using cabal 8.10.4 version 
# by specifying the  particular compiler to be used.
cabal update
cabal configure --with-compiler=ghc-8.10.4
```

```
# addinng extra flages for libsodium library
echo "package cardano-crypto-praos" >>  cabal.project.local
echo "  flags: -external-libsodium-vrf" >>  cabal.project.local
```

```
# now let's compile the code
cabal build all
```

And now we wait...  it could take some while (1h+ ) to compile, depending on your server's CPU&#x20;

![](https://media3.giphy.com/media/2uwZ4xi75JhxZYeyQB/giphy.gif?cid=ecf05e47cuuc11ypr2nr7rd48wieckoimcj9018ykxtsr6nc\&rid=giphy.gif\&ct=g)

{% hint style="warning" %}
Before the next step -  STOP your node so it doesn't lock the carano-node file for overwriting
{% endhint %}

```
sudo systemctl stop cardano-node
```

```
# moving the freshly compiled binaries to bin folder 
mkdir -p ~/.local/bin/
cp -p dist-newstyle/build/x86_64-linux/ghc-8.10.4/cardano-cli-1.34.1/x/cardano-cli/build/cardano-cli/cardano-cli ~/.local/bin/
cp -p dist-newstyle/build/x86_64-linux/ghc-8.10.4/cardano-node-1.34.1/x/cardano-node/build/cardano-node/cardano-node ~/.local/bin/
```

```
# let's check if we have successfully installed the latst cardano-node and cardano-cli versions.
which cardano-node && which cardano-cli
cardano-node --version
cardano-cli --version
```

you should now have similar output:

![](<../.gitbook/assets/CleanShot 2022-03-11 at 15.29.09@2x.png>)

Now we can start the cardano node process

```
sudo systemctl start cardano-node
```

and check the log files if everything is starting up as planned:

```
journalctl -u cardano-node.service -f -o cat
```

![](<../.gitbook/assets/CleanShot 2021-09-29 at 17.24.47@2x.png>)

**that's it - you have upgraded your node to the latest cardano-node version, now do the same update on all of your other production servers (or copy generated cardano-cli / cardano-node bin files).**

{% hint style="info" %}
Need help?\
👉🏼 Join our Telegram support Group: [https://t.me/StakePool247help](https://www.youtube.com/redirect?event=video\_description\&redir\_token=QUFFLUhqbFFLWlhNYkhpRlhYd3gyWkIwbU91R2ZhUmZzUXxBQ3Jtc0tuUko0cnVvanYwVktab1FWalVMb0ZOVEpmTDBNRXNSRWwwbWk0UE5tdkZYRENDZWRBYjlxMVYxMTdqdjBfeDB3WmhiTDRjNm13RDVSeDhDQ0JEOWZfVUlEX1RaRm10UlJsWXZkTzdIY29aeTEtMnN3aw\&q=https%3A%2F%2Ft.me%2FStakePool247help)
{% endhint %}

****
