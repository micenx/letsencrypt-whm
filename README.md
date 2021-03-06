# What is this?

This is respository for shell script to automate installation [Let's Encrypt](https://letsencrypt.org/) SSL certificates generated by `certbot-auto`
into WHM-based Linux server.

# Motivation

Latest WHM adds [Let's Encrypt](https://letsencrypt.org/) SSL certificate plugin,
however [CPanel](https://cpanel.com/) dropped support for Centos 6 32-bit system.

This is for WHM user who stuck on WHM version < 58 but want to use
Let's Encrypt SSL certificates automated domain validation tools.

# Requirement

- SSH access to WHM-based server with administrative privilege.
- `certbot-auto` [Installation Guide](https://certbot.eff.org/docs/install.html)
- [PHP](https://php.net)
- `git`
- [WHM API 1 Install Ssl](https://documentation.cpanel.net/display/DD/WHM+API+1+Functions+-+installssl)

# Installation

Login to SSH and clone this repository.

# Usage

## Install Certificates

    # ./letsencrypt.whm.ssl.install.sh [working directory] [domain name]

`[working directory]` is web root directory of `[domain name]` to store
temporary http challenge for domain validation. `[domain name]` is domain name
to generate certificate.

    # ./letsencrypt.whm.ssl.install.sh /home/userxxx/public_html example.com

If you install `certbot-auto` in directory that is not in `PATH` environment variable then you can specify absolute path using `CERTBOT_EXEC` variable. For example

    # CERTBOT_EXEC=/usr/local/certbot/certbot-auto ./letsencrypt.whm.ssl.install.sh /home/userxxx/public_html example.com

## Renew Certificates

    # ./letsencrypt.whm.renew.sh

If you install `certbot-auto` in directory that is not in `PATH` environment variable then you can specify absolute path using `CERTBOT_EXEC` variable. 

```
# CERTBOT_EXEC=/path/to/certbot-auto ./letsencrypt.whm.renew.sh
```

For example

```
# CERTBOT_EXEC=/usr/local/letsencrypt/certbot-auto ./letsencrypt.whm.renew.sh
```

`letsencrypt.wh.renew.sh` is script that you need to run periodically with cron
to avoid issue with expired SSL certificates. This script calls `certbot-auto renew`
command. It is save to call this periodically as explained [here](
https://certbot.eff.org/docs/using.html#renewing-certificates).

> Unlike certonly, renew acts on multiple certificates and always takes into account whether each one is near expiry. Because of this, renew is suitable (and designed) for automated use, to allow your system to automatically renew each certificate when appropriate. Since renew only renews certificates that are near expiry it can be run as frequently as you want - since it will usually take no action.

## Install SSL Certificate manually

If you already have Lets Encrypt SSL certificate generated, you can manually
install the certificate without generating new certificate.

`whm.install.cert.sh` installs existing Lets Encrypt SSL certificate for a domain name.

    # ./whm.install.cert.sh [domain name]


Zamrony P. Juhara
