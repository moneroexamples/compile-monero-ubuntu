# Compile Monero on Ubuntu 14.04 x86_64
The example shows how to compile current github version of [Monero](https://getmonero.org/), as of 31 Oct 2015,
on Ubuntu 14.04 x86_64.

## Preparation
Before proceeding to the compilation, the following packages are required:

 ```bash
# refresh ubuntu's repository
sudo apt-get update

#install git
sudo apt-get install git

# install dependencies
sudo apt-get install build-essential cmake libboost1.55-all-dev miniupnpc libunbound-dev graphviz doxygen libdb5.1++-dev
 ```

## Compilation
Having the dependencies, we can download the current Monero version and compile it as follows:

```bash
# download the latest bitmonero source code from github
git clone https://github.com/monero-project/bitmonero.git

# go into bitmonero folder
cd bitmonero/

# compile
# cmake . #  optional for configuration and checking what is available or missing
make # or make -j number_of_threads, e.g., make -j 2
```
## Instalation (optional)
After successful compilation, the Monero binaries should be located in `./bin`

I usually move the binaries into `/opt/bitmonero/` folder. This can be done
as follows:

```bash
# optional
sudo mkdir /opt/bitmonero
sudo mv ./build/release/bin/* /opt/bitmonero/
```

Now we can start the Monero daemon and let it
download the blockchain and synchronize itself with the Monero network. After that, you can run your the simplewallet.

```bash
# launch the Monero daemon and let it synchronize with the Monero network
/opt/bitmonero/bitmonerod

# launch the Monero wallet
/opt/bitmonero/simplewallet
```

## Command hisotry and tab completion
Both simplewallet and bitmonerod are command line programs, and they do
not support command history and tab completion. This can be annoying for
linux users, who are usually accustomed to these features in a command line.

This problem can be overcome using [rlwrap](https://github.com/hanslub42/rlwrap).
The rlwrap requires a file with a list of commands to be used in tab
completion. The files can be downloaded here:

 - [monerocommands_bitmonerod.txt](https://github.com/moneroexamples/compile-monero-ubuntu/blob/master/monerocommands_bitmonerod.txt)
 - [monerocommands_simplewallet.txt](https://github.com/moneroexamples/compile-monero-ubuntu/blob/master/monerocommands_simplewallet.txt)


```bash
# install rlwrap
sudo apt-get install rlwrap

# download the commands files, for example, to your home folder
cd ~
wget https://raw.githubusercontent.com/moneroexamples/compile-monero-ubuntu/master/monerocommands_bitmonerod.txt

wget https://raw.githubusercontent.com/moneroexamples/compile-monero-ubuntu/master/monerocommands_simplewallet.txt

# having the file for the daemon, it can be run as follows:
rlwrap -f monerocommands_bitmonerod.txt /opt/bitmonero/bitmonerod

# having the file for the wallet, it can be run as follows:
rlwrap -f /path/to/monerocommands_simplewallet.txt /opt/bitmonero/simplewallet

```

Probaly easier to make aliases into your ~/.bashrc, for example:

```bash
# add this to the end of your ~/.bashrc
alias moneronode="rlwrap -f monerocommands_bitmonerod.txt /opt/bitmonero/bitmonerod"
alias monerowallet="rlwrap -f monerocommands_simplewallet.txt /opt/bitmonero/simplewallet"
```

## How can you help?

Constructive criticism, code and website edits are always good. They can be made through github.

Some Monero are also welcome:
```
48daf1rG3hE1Txapcsxh6WXNe9MLNKtu7W7tKTivtSoVLHErYzvdcpea2nSTgGkz66RFP4GKVAsTV14v6G3oddBTHfxP6tU
```
