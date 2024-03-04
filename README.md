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
