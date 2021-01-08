# oracle-11g-server-action

[![Build](https://github.com/GoodManWEN/oracle-11g-server-action/workflows/Build/badge.svg)](https://github.com/GoodManWEN/oracle-11g-server-action/actions?query=workflow:Build)

This [GitHub Action](https://github.com/features/actions) sets up a Oracle database server in Docker container.

Based on [Oracle 11gR2 image on dockerhub](https://hub.docker.com/r/oracleinanutshell/oracle-xe-11g), which is built on ubuntu 18.04 . There're very limited options we could modify on startup for the original image , so that this action could only be suitable for basic testing.

It should be noted that this action sets up Oracle db server only , you must set up a Oracle client yourself as well in order to access to the server. For further information you can check out [this repo](https://github.com/GoodManWEN/oracle-client-action.git) as example

It is based on the Docker container and is limited by Github Actions, which contains only Linux now. Therefore it does not work in Mac OS and Windows environment.

## Usage
```
steps:
  - name:Checkout
    uses: actions/checkout@v2 # You need to checkout first, then you can use your repo in following actions.
    with:
      repository: GoodManWEN/oracle-client-action
  - name: Setup Oracledb client
    uses: GoodManWEN/oracle-client-action@main
  - name: Checkout
    uses: actions/checkout@v2
    with:
      repository: GoodManWEN/oracle-11g-server-action
  - name: Setup Oracledb 11gR2 server
    uses: GoodManWEN/oracle-11g-server-action@main
    with:
      host port: 1521         # Which means the reflect port on your host.
      oracle version: '1.0.0' # Means not version of oracle , but the version of dockerhub image.
```
Then you can connect database with following setting:
```
hostname: localhost
port: 1521
sid: xe
username: system
password: oracle
```
Unfortunately you can not modify sid nor password yourself before startup.

## Licence

This project is released under the [MIT License](https://github.com/GoodManWEN/oracle-11g-server-action/blob/main/LICENSE).
