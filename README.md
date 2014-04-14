ansible-rabbitmq
=================

Playbook for provisioning RabbitMQ on an Ubuntu server (tested on 12.04) with
management console enabled.

Includes an IPTables firewall ready for DigitalOcean use (IPv4, SSH
port whitelisted on public eth0, ports 5672 and 15672 whitelisted on
private eth0).

Also includes a Vagrant config for development testing using [vagrant-lxc][1].

[1](https://github.com/fgrehm/vagrant-lxc)
