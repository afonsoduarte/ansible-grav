# ansible-grav

Ansible playbooks for setting up a LE(M)P stack for Grav.

- Local development environment with Vagrant
- High-performance production servers
- One-command deploys

These playbooks were shamelessly ripped off from the excellent [Trellis](https://roots.io/trellis/), a collection of ansible playbooks for a WordPress server.

## What's included

These playbooks will configure a server with the following and more:

* Ubuntu 14.04 Trusty LTS
* Nginx (with optional FastCGI micro-caching)
* PHP 7.0
* SSL support (scores an A+ on the [Qualys SSL Labs Test](https://www.ssllabs.com/ssltest/))
* Let's Encrypt integration for free SSL certificates
* HTTP/2 support (requires SSL)
* Composer
* WP-CLI
* sSMTP (mail delivery)
* MailHog
* Memcached
* Fail2ban
* ferm

## Requirements

Make sure all dependencies have been installed before moving on:

* [Ansible](http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-pip) >= 2.0.0.2
* [Virtualbox](https://www.virtualbox.org/wiki/Downloads) >= 4.3.10
* [Vagrant](http://www.vagrantup.com/downloads.html) >= 1.5.4
* [vagrant-bindfs](https://github.com/gael-ian/vagrant-bindfs#installation) >= 0.3.1 (Windows users may skip this)
* [vagrant-hostmanager](https://github.com/smdahlen/vagrant-hostmanager#installation)

## Installation

The recommended directory structure looks like:

```shell
example.com/          # → Root folder for the project
├── ansible-grav/     # → Your clone of this repository
└── site/             # → Grav folder
```


1. Create a new project directory: `$ mkdir example.com && cd example.com`
2. Clone ansible-grav: `$ git clone --depth=1 git@github.com:afonsoduarte/ansible-grav.git && rm -rf ansible-grav/.git`
3. Install the Ansible Galaxy roles: `$ cd ansible-grav && ansible-galaxy install -r requirements.yml`
3. Download Grav: <https://getgrav.org/downloads>, unpack, rename folder to `site`, and put it in your project root folder

## Documentation

This project does not have its own documentation. Instead, please check the [Trellis documentation](https://roots.io/trellis/docs/) on which this project is based.

## Local development setup

1. Configure your Grav sites in `group_vars/development/grav_sites.yml` and in `group_vars/development/vault.yml`
2. Run `vagrant up`

[Read the local development docs](https://roots.io/trellis/docs/local-development-setup/) for more information.

## Remote server setup (staging/production)

A base Ubuntu 14.04 server is required for setting up remote servers.

1. Configure your Grav sites in `group_vars/<environment>/grav_sites.yml` and in `group_vars/<environment>/vault.yml` (see the [Vault docs](https://roots.io/trellis/docs/vault/) for how to encrypt files containing passwords)
2. Add your server IP/hostnames to `hosts/<environment>`
3. Specify public SSH keys for `users` in `group_vars/all/users.yml` (see the [SSH Keys docs](https://roots.io/trellis/docs/ssh-keys/))
4. Run `ansible-playbook server.yml -e env=<environment>` to provision the server

[Read the remote server docs](https://roots.io/trellis/docs/remote-server-setup/) for more information.

## Deploying to remote servers

1. Add the `repo` (Git URL) of your Grav project in the corresponding `group_vars/<environment>/grav_sites.yml` file
2. Set the `branch` you want to deploy
3. Run `./deploy.sh <environment> <site name>`
4. To rollback a deploy, run `ansible-playbook rollback.yml -e "site=<site name> env=<environment>"`

[Read the deploys docs](https://roots.io/trellis/docs/deploys/) for more information.

## Contributing

Contributions are welcome from everyone. We have [contributing guidelines](CONTRIBUTING.md) to help you get started.

## Community

Keep track of development and community news.

* Participate on the [Roots Discourse](https://discourse.roots.io/)
* Follow [@rootswp on Twitter](https://twitter.com/rootswp)
* Read and subscribe to the [Roots Blog](https://roots.io/blog/)
* Subscribe to the [Roots Newsletter](https://roots.io/subscribe/)
* Listen to the [Roots Radio podcast](https://roots.io/podcast/)
