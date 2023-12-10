**Ansible Role Certbot**
========================

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=flat&logo=ansible&logoColor=white)
![GitHub License](https://img.shields.io/github/license/ironwolphern/ansible-role-certbot)
![GitHub release (with filter)](https://img.shields.io/github/v/release/ironwolphern/ansible-role-certbot)
![GitHub pull requests](https://img.shields.io/github/issues-pr/ironwolphern/ansible-role-certbot)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/ironwolphern/ansible-role-certbot)
![GitHub issues](https://img.shields.io/github/issues/ironwolphern/ansible-role-certbot)
[![Ansible Lint](https://github.com/ironwolphern/ansible-role-certbot/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/ironwolphern/ansible-role-certbot/actions/workflows/ansible-lint.yml)
![Dependabot](https://badgen.net/github/dependabot/ironwolphern/ansible-role-certbot)

This is an Ansible role to install and configure Certbot to generate certificates of Let´s Encrypt in your server. For more information
of Let´s Encrypt and Certbot please visit the official website: https://letsencrypt.org and https://certbot.eff.org
For the official documentation for more options visit the website: https://certbot.eff.org/docs

*Requirements*
--------------

This role need the snap installer, if not installed in your OS, the role will install it. Some modules in role tasks need to be use with an ansible collection ***community.general*** for install and use snap and ***community.crypto*** for create a private key and csr to deploy certificate with custom data.

You can install this collections with requirements file:
```shell
  ansible-galaxy collection install -r requirements.yml
```

Too the community.crypto modules need the following library installed:

cryptography >= 1.3


*Role Variables*
----------------

This is a list of required and optinal variables and parameters for this role:

| **Parameter** | **Description** | **Type** | **Default** | **Options** | **Required** |
|---------------|-----------------|----------|:-----------:|:-----------:|:------------:|
| certbot__agree_tos | Agree to the terms of service of Let´s Encrypt | boolean | true | true/false | no |
| certbot__curve | Curve to use for the ECDSA certificate key | string | secp384r1 | Please see RFC 8446 for supported values | no |
| certbot__email | Email to register in Let´s Encrypt | string | '' | | yes |
| certbot__key_size | Size of the key | integer | 4096 | | no |
| certbot__key_type | Type of the key | string | ecdsa | rsa/ecdsa | no |
| certbot__domains | List of domains to generate the certificate | list | [] | | yes |
| certbot__server | Server to use for sign the certificate | string | https://acme-staging-v02.api.letsencrypt.org/directory | https://acme-staging-v02.api.letsencrypt.org/directory / https://acme-v02.api.letsencrypt.org/directory | no |
| certbot__cert_path | Path to store the certificate | string | /etc/letsencrypt/live | | no |
| certbot__key_path | Path to store the key | string | /etc/letsencrypt/live | | no |
| certbot__fullchain_path | Path to store the fullchain | string | /etc/letsencrypt/live | | no |
| certbot__chain_path | Path to store the chain | string | /etc/letsencrypt/live | | no |
| certbot__archive_path | Path to store the archive | string | /etc/letsencrypt/archive | | no |
| certbot__user | User to security path of the certbot | string | root | | no |
| certbot__group | Group to security path of the certbot | string | root | | no |
| certbot__dns_provider | DNS provider to use for validation (dns-01) | string | standalone | standalone, cloudflare, digitalocean, dnsimple, dnsmadeeasy, gehirn, google,linode, luadns, nsone, ovh, rfc2136, route53, sakuracloud | no |
| certbot__dns_provider_token | Token to use for the DNS provider API (dns-01) | string | '' | | no |
| certbot__dns_provider_dir_credentials | Path to store the credentials of the DNS provider (dns-01) | string | /etc/letsencrypt/dns | | no |
| certbot__dns_provider_propagation_seconds | Seconds to wait for the propagation of the DNS provider (dns-01) | integer | 10 | | no |
| certbot__tls_selfsigned_csr_country | Country of the CSR | string | ES | | no |
| certbot__tls_selfsigned_csr_state | State of the CSR | string | Madrid | | no |
| certbot__tls_selfsigned_csr_locality | Locality of the CSR | string | Madrid | | no |
| certbot__tls_selfsigned_csr_organization | Organization of the CSR | string | My Company | | no |
| certbot__tls_selfsigned_csr_ou | Organizational Unit of the CSR | string | Departament | | no |
| certbot__tls_selfsigned_csr_sans | List of Subject Alternative Names of the CSR | list | [] | email, URI, DNS, RID, IP, dirName, otherName | no |
| certbot__tls_csr | Flag to use CSR | boolean | false | true/false | no |
| certbot__tmp_dir | Temp directory for role | string | /tmp/certbot | | no |
| certbot__debugger | Flag to activate debugger | boolean | false | true/false | no |

*Dependencies*
--------------

There are no dependencies.

*Example Playbook*
------------------

This is an example of use role with optionals and required parameters:

*play-certbot.yml*
```yaml
- hosts: certbot
  gather_facts: true
  roles:
    - role: ansible-role-certbot
      vars:
        certbot__email: demo@example.local
        certbot__dns_provider: standalone
        certbot__domains:
          - example.local
```

These are some examples of the use of this playbook with the different tags that can be used in this role:

Install and configure full
```shell
  ansible-playbook -i inventory play-certbot.yml
```
Uninstall
```shell
  ansible-playbook -i inventory play-certbot.yml -t uninstall
```
Deploy certificate for domains in playbook vars
```shell
  ansible-playbook -i inventory play-certbot.yml -t deploy
```
Undeploy certificates
```shell
  ansible-playbook -i inventory play-certbot.yml -t undeploy
```

*License*
---------

MIT

*Author Information*
--------------------

This role was created in 2023 by:

- Fernando Hernández San Felipe (ironwolphern@outlook.com)
