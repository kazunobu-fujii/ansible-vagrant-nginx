# nginx on vagrant (precise32)

## Install ansible

https://devopsu.com/guides/ansible-mac-osx.html

```
$ sudo easy_install pip
$ sudo pip install ansible --quiet
```

## Get source code

clone me

```
$ git clone git@github.com:kazunobu-fujii/ansible-vagrant-nginx.git
$ cd ansible-vagrant-postfix
```

## Prepare vagrant

```
$ vagrant up
```

You can access `http://0.0.0.0:3000` via `http://192.168.33.31` and `https://192.168.33.31`.

```
$ open http://192.168.33.31
$ open https://192.168.33.31
```

## Configuration

### Server

- HTTP: 192.168.33.31:80
- HTTPS: 192.168.33.31:443
- Proxy to: 192.168.33.1:3000 (0.0.0.0:3000)

### SSL certification

Install own singed SSL certification to avoid browser warning.

```
$ scp vagrant@192.168.33.31:/etc/nginx/ssl/server.crt .
```

## Customize

Please refer `Vagrant` and `playbook.yml`.

To change VM `ip address`.

```ruby:Vagrant
node.vm.network "private_network", ip: "192.168.33.31"
```

To change `proxy_pass`.

```YAML:playbook.yml
vars:
  proxy_pass: http://192.168.33.1:3000
```
