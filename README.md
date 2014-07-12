raichuserver
============
Simple Vagrant+Docker files to create a homeserver.

Requisites
----------

 - Ubuntu 14.04
 - Vagrant (1.6.3)
 - Docker (0.9.1)

Usage
-----

### MySQL Server

Based in https://github.com/tutumcloud/tutum-docker-mysql

```
git clone... submodule init... update... etc etc
cd vagrant_machines/mysql
sudo vagrant up --provider=docker
```

Initial random password for root user in MySQL ('PASSWORD' in the example):
```
sudo vagrant docker-logs
[...]
========================================================================
==> default: You can now connect to this MySQL Server using:
==> default:
==> default:     mysql -uadmin -pPASSWORD -h<host> -P<port>
==> default:
==> default: Please remember to change the above password as soon as possible!
==> default: MySQL user 'root' has no password but only allows local connections
==> default: ========================================================================
[...]

mysqladmin -uadmin -pPASSWORD -h127.0.0.1 password NEW_PASSWORD
```

### Apache2 + PHP5 + OwnCloud Server

Based in https://github.com/yankcrime/dockerfiles

```
cd vagrant_machines/owncloud
sudo vagrant up --provider=docker
```

### Shipyard Server

Web UI to manage Docker containers/images in a set of hosts

```
cd vagrant_machines/shipyard-server
sudo vagrant up --provider=docker
```

Now, access: http://server:8000

### Shipyard Agent for each host

```
cd vagrant_machines/shipyard-agent
sudo vagrant up --provider=docker
```

Now, enable host from Shipyard UI.

