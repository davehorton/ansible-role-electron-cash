# ansible-role-electron-cash 

This is an ansible role for building a headless [Electron Cash](https://electroncash.org/). 

**Important:** Note that it builds and installs electron-cash, and also creates a systemd service file for starting and stopping electron-cash.  It does not create a default wallet for you, so after install you will want to manually do that by running `electron-cash create` in your inital session after install.  Likewise, running `systemctl start electron-cash` will start the electron-cash daemon but you will then need to manually load your wallet by running `electron-cash daemon load_wallet`.  This is done for security purposes.

This ansible role has only been tested on Debian 9.

## Role variables

Available variables are listed below, along with default values (see defaults/main.yml):
```
electron_cash_version: 3.3
```
version of Electron Cash to download and install

```
electron_cash_rpc_port: 7777
```
tcp port to listen on for rpc calls
```
electron_cash_rpc_user: user
```
the username for authentication of rpc requests.
```
electron_cash_rpc_password: changeme
```
the password for authentication of rpc requests.

## Example playbook
```
---
- hosts: all
  become: yes
  vars_prompt:

  - name: "electron_cash_rpc_user"
    prompt: "Please give a username to use when authenticating rpc requests"
    default: "user"  

  - name: "electron_cash_rpc_password"
    prompt: "Please give a password to use when authenticating rpc requests"
    default: "changeme"  

  - name: "electron_cash_rpc_port"
    prompt: "Please give the tcp port to listen on for rpc requests"
    default: 7777

  roles:
    - ansible-role-electron-cash
```
