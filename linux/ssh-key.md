---
title: Generating SSH Keys and Copy Public Keys
date: 2019-05-27
tags: ssh shell secured key
---

# ssh
## host/user alias
Edit $HOME/.ssh/config
````sh
cat $HOME/.ssh/config
host my_alias  # this is the alias name
    hostname some.host.remote  # real host name
    user john # optional, otherwise use john@my_alias
````

## create ssh-key

````sh
ssh-keygen
````
ssh-keygen generates a pair of RSA key (private id_rsa and public id_rsa.pub) at $HOME/.ssh

## copy the public key file to remote host (john@host.remote)
````sh
ssh-copy-id -i ~/.ssh/id_rsa.pub john@host.remote
````
The command add an entry in ~/.ssh/authorized_keys on the remote host. After the public key is added, you can ssh login without password.
````sh
ssh john@host.remote
````
