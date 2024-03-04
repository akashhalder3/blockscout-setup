# Blockscout setup in Ubuntu

## Environment

- **Operating System:** Ubuntu 18.04.6 LTS (GNU/Linux 4.15.0-177-generic x86_64)
- **Server Hardware:** ProLiant DL585 G7
- **Database Server:** PostgreSQL 10.19 (Ubuntu 10.19-0ubuntu0.18.04.1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 7.5.0-3ubuntu1~18.04) 7.5.0, 64-bit

This guide will walk you through the process of setting up Blockscout on Ubuntu. Blockscout is an open-source blockchain explorer for Ethereum-based networks. By following these steps, you'll be able to deploy Blockscout and explore Ethereum blockchains with ease. Let's get started!

### DB Server

```bash
$ sudo apt-get update
$ sudo apt install postgresql postgresql-contrib
$ sudo -u postgres psql -c "SELECT version();"
$ sudo apt update
$ sudo apt -y install erlang
$ erl --version
```

### Add erlang repos
```bash
$ cd ~
$ sudo apt install curl software-properties-common apt-transport-https lsb-release
$ curl -1sLf 'https://dl.cloudsmith.io/public/rabbitmq/rabbitmq-erlang/setup.deb.sh' | sudo -E bash
```

### Install specific versions of Erlang and Elixir
```bash
$ sudo apt update
$ sudo apt install erlang
$ sudo apt install elixir
```

### Install Nodejs
```bash
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
$ source ~/.bashrc
$ nvm list-remote
$ nvm install v20.11.0
```

### Install Rust
```bash
$ sudo curl https://sh.rustup.rs -sSf | sh -s -- -y
$ rustc --version
$ sudo reboot
```

### Install Cargo
```bash
$ sudo apt install cargo
```

### Install Other dependancies
```bash
$ sudo apt -y install automake libtool inotify-tools gcc libgmp-dev make g++ git
```

### set environment variables
```bash
export SECRET_KEY_BASE=VTIB3uHDNbvrY0+60ZWgUoUBKDn9ppLR8MI4CpRz4/qLyEFs54ktJfaNT6Z221No
export ETHEREUM_JSONRPC_VARIANT=geth
export ETHEREUM_JSONRPC_HTTP_URL=http://20.193.151.164:8545
export ETHEREUM_JSONRPC_TRACE_URL=http://20.193.151.164:8545
export ETHEREUM_JSONRPC_WS_URL=ws://20.193.151.164:8546
export DATABASE_URL=postgresq://dbuser:1234@localhost:5432/blockscout
export COIN=pos
```
### clone and compile Blockscout
```bash
$ git clone https://github.com/poanetwork/blockscout.git
$ cd blockscout/
$ mix local.hex --force
$ mix do deps.get, local.rebar --force, deps.compile
$ mix compile
```
### Migrate DB
```bash
$ mix do ecto.create, ecto.migrate
$ mix do ecto.drop, ecto.create, ecto.migrate # for drop and remigrate
```

### Install npm dependancies and compile frontend assets
```bash
$ Install npm dependancies and compile frontend assets
$ cd apps/explorer && npm install; cd -
```
### SSL to the dev environmen
``bash
$ cd apps/block_scout_web
$ mix phx.gen.cert blockscout blockscout.local
```

### Reference 
1. https://sayboy.ddns.net/p/blockscout/ by Di Xu
2. https://docs.blockscout.com/for-developers/deployment/manual-deployment-guide
