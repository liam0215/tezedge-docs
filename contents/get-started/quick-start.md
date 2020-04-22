---
title: Quick Start
sidebar: Docs
showTitle: false
---

Quick start
------------

**Pre-requisites**

* GitHub repository 

* Docker

Open shell and type this code into the command line and then press Enter:

```
git clone https://github.com/simplestaking/tezedge
cd tezedge
```

**1. Download and install Docker and Docker Compose**

Open shell and type this code into the command line and then press Enter:

```
docker-compose pull
docker-compose up
```

![alt text](https://raw.githubusercontent.com/simplestaking/tezedge/master/docs/images/node_bootstrap.gif)

**2. Open the TezEdge Explorer in your browser** 

You can view the status of the node in your browser by entering this address into your browser's URL bar:

http://localhost:8080

![alt text](https://raw.githubusercontent.com/simplestaking/tezedge/master/docs/images/explorer_bootstrap.gif)

Building from Source
------------

**1. Install rustup command** 

We recommend installing Rust through rustup.

Run the following in your terminal, then follow the onscreen instructions.

```
curl https://sh.rustup.rs -sSf | sh
```

**2. Install rust toolchain** 

Rust nightly is required to build this project.
```
rustup toolchain install nightly-2020-02-04
rustup default nightly-2020-02-04
```

**3. Install required libs**

Install libs required to build sodiumoxide package:
```
sudo apt install pkg-config libsodium-dev
```

Install libs required to build RocksDB package:
```
sudo apt install clang libclang-dev llvm llvm-dev linux-kernel-headers libev-dev
```

**4. Supported Linux distributions**

We are linking rust code with pre-compiled Tezos shared library. For your convenience we have created pre-compiled binary files
for most of the popular linux distributions:

supported linux distributions:
* Ubuntu (16.04, 18.04, 18.10, 19.04)
* Debian (9, 10 )
* OpenSUSE (15.1, 15.2)
* CentOS (6, 7, 8)
    
If you are missing support for your favorite linux distribution on a poll request at [tezos-opam-builder](https://github.com/simplestaking/tezos-opam-builder) project.


Running node manually
----------------

The node can built through the `cargo build` or `cargo build --release`, be aware, release build can take 
much longer to compile. environment variable `SODIUM_USE_PKG_CONFIG=1` mus be set. Put together, node can be build, for example, like this:
```
SODIUM_USE_PKG_CONFIG=1 cargo build
```

To run node manually, path to the Tezos lib must be provided as environment variable `LD_LIBRARY_PATH`. It is required
by `protocol-runner`. Put together, node can be run, for example, like this:
```
LD_LIBRARY_PATH=./tezos/interop/lib_tezos/artifacts cargo run --bin light-node -- --config-file ./light_node/etc/tezedge/tezedge.config
```

All parameters can be provided also as command line arguments in the same format as in config file, in which case 
they have higher priority than the ones in config file. For example we can use the default config and change the log file path:
```
LD_LIBRARY_PATH=./tezos/interop/lib_tezos/artifacts cargo run --bin light-node -- --config-file ./light_node/etc/tezedge/tezedge.config --log-file /tmp/logs/tezdge.log
```

Full description of all arguments is in the light_node [README](light_node/README.md) file.



Running node using run.sh script
----------------


On linux systems, we prepared convenience script to run the node. It will automatically set all necessary environmnent variables, build and run tezedge node. 
All arguments can be provided to the `run.sh` script in the same manner as described in the previous section - Running Tezedge node manually.

The following command will execute node in debug node:

```
./run.sh node
```

To run node in release mode execute the following:

```
./run.sh release
```

If you are running OSX you can use docker version:

```
./run.sh docker
```

Listening for updates. Node emits statistics on the websocket server, which can be changed by `--websocket-address` argument, for example:

```
./run.sh node --websocket-address 0.0.0.0:12345
```
