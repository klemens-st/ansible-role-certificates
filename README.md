Ansible role: Certificates
=========

An Ansible role that installs custom certificates on Debian/Ubuntu.

Requirements
------------

The role does not generate or download any certificates, you need to provide your own. You can generate a self-signed certificate with a command like `openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout example.key -out example.crt`.

Make sure the certificates are in an appropriate format, this role does not convert certificates. E.g. CA certificates should be in PEM format.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
certificates_install_ca: false
certificates_install_certs: false
```
By default the role does nothing. Setting the first variable to `true` enables custom CA certificates installation, the second variable enables custom certs and keys.

```yaml
certificates_ca_path: "/usr/local/share/ca-certificates/ansible"
```
Default path for ansible managed custom CA certificates.

```yaml
certificates_ca_certs:
  - path/to/ca/cert
  - path/to/another/ca
```
List of custom CA certs to install. Empty by default.

```yaml
certificates_certs_path: "/etc/ssl/certs"
certificates_keys_path: "/etc/ssl/private"
```
Default paths for custom certificates and keys.

```yaml
certificates_certs:
- cert: path/to/Example.crt
  key: path/to/Example.key
```
List of custom certificates and keys to install. Empty by default.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```yaml
- hosts: servers
  roles:
    - klemens-st.certificates

  vars:
    certificates_install_ca: true
    certificates_install_certs: true
    certificates_ca_certs:
     - files/MySpecialCA.crt
    certificates_certs:
      cert: files/server.pem
      key: files/server.key

```

License
-------

MIT

Author Information
------------------

This role was created in 2025 by Klemens Starybrat.
