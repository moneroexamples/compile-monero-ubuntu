# Compile Monero on Whonix-Workstation for VirtualBox
[Monero](https://getmonero.org/) and [Whonix](https://www.whonix.org/) are tools
that privacy centric users can use as part of their privacy enchancing toolbox.

One problem with Monero is that, if you want to run full Monero node, your
IP address will be exposed to others in the Monero network. This, for some,
might be not very good idea.

One way to overcome this problem is to run the node through Tor. And this can be done having the Monero node runnign insde the Whonix.

Is this the best solution possible? Probobably not, as runige node in VirtualBox through tor can be slow (depending on your computer). In future, Monero will solve this problem by incorporating [i2p support](https://forum.getmonero.org/1/news-announcements-and-editorials/208/why-we-chose-i2p-over-tor).

## Preparation
 Assuming that you have Whonix setup into your VirtualBox, the first thing that
 should be done is to increase Whonix-Workstation's ram. The default size
 is 768 MB this is not enough. I usually set it up to 2 GB, but I think 1GB
 should also be enough.

 ```bash
 VBoxManage modifyvm Whonix-Workstation --memory 2048
 ```

## Compilation
Start your Whonix-Workstation and do the following in the workstation.

```bash
# install dependencies
sudo apt-get install build-essential cmake libboost1.55-all-dev miniupnpc  libunbound-dev graphviz doxygen liblmdb-dev

# download the latest bitmonero source code from github
git clone https://github.com/monero-project/bitmonero.git

# go into bitmonero folder
cd bitmonero/

# compile
cmake .
make
```

After successful compilation, the Monero binaries should be located in `./bin`

I usually move the binaries into `/opt/bitmonero/` folder, so this can be done
as follows:
```
sudo mkdir /opt/bitmonero
sudo mv ./bin/* /opt/bitmonero/
```

To start now the only think left is to start the Monero deamon and let it
download the blockchain and synchronize with the Monero network. After that,
you can run your the simplewallet.

Please note that downloading the full blockchain (over 7 GB as of October 2015) will probably be very slow. So it would be better to get download it independelty
and then copy to the default monero folder, i.e., `~/.bitmonero/lmdb/`

```
# launch the monero node demon and let it synchronize with the monero network
/opt/bitmonero/bitmonerod

# launch the monero wallet
#/opt/bitmonero/simplewallet
