# simple-ansible-apache

Hi,

this is my simple ansible apache2 role. With this role you can install and configure an apache2 webserver under the following operating systems:

* Debian (>7)
* Ubuntu (>14.04)
* RHEL
* CentOS (>6.7)

## Configuration / Usage

The role will automatically chose the platform specific install and configuration files. Each platform has its own set of variables set in the vars.yml under the vars section. With the examples included, it will automatically create two virtualhosts (I´ve put this in for a better understanding of the variables/usage of the variables)

### Variable configuration

#### Variables

Below a short description of the used variables and their purpose:

```
httpd_packages/apache2_packages
```
Set of platform specific packages to be installed


```
apache2_modules
```
Debian/Ubuntu-specific: Set of apache2 modules to be enabled by default


```
apache2_virtualhosts:
  - name: virtualhost01.example.com
    owner: vagrant
    group: www-data
    docroot: /var/www/virtualhost01.example.com/htdocs
    docpath: /var/www/virtualhost01.example.com
    sslpath: /etc/ssl/localcerts/
    sslcertificatefile: virtualhost01.example.com.crt
    sslcertificatekeyfile: virtualhost01.example.com.key
    logdir: /var/log/apache2/
```
- name: name of the virtualhost, also used as certificate CN
- owner: owner of the document root / path
- group: group to bet set for document root / path
- docroot: main document root for virtualhost (htdocs directory)
- docpath: path where the docroot will be
- sslpath: path to the ssl certificate (will be used for the self-signed certificates, too)
- sslcertificatefile: name of the ssl certificate file (crt)
- sslcertificatekeyfile: name of the ssl certificate key (key)
- logdir: log directory for virtualhost specific logs

#### Switches
There are some switches defined in the variables files with the below functionality:

```
sslvhosts
```
Can be true or false. When true it will create the self-signed certificates and ssl part of the virtualhost.

```
apache_create_virtualhosts
```
Can be true or false. When false, no virtualhosts will be created.

```
firewalldrules
```
For Systems with firewalld installed/enabled - can be true or false. When true it will automatically set the httpd/https rules (permanent) at the firewall.
