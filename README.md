Nextcloud Ansible role
======================

An Ansible role to install and configure Nextcloud, with Apache and PostgreSQL. Works on Debian-based distributions.

Requirements
------------

This role doesn't add, manage or configure SSL certificates for Apache. If you choose to enable SSL (you should), Apache should be configured appart from this role to use the right SSL certificate. I made this choice to be able to manage everything related to SSL certs in another separate configuration file.

Role Variables
--------------

All the variables for the role are described below along with their default values.

- Database configuration: database name, username and password
```yaml
nextcloud_database_name: nextcloud
nextcloud_database_username: nextcloud
nextcloud_database_password: nextcloud
```

- Credentials for the default admin account
```yaml
nextcloud_admin_username: admin
nextcloud_admin_password: nextcloud
```

- Download URL for Nextcloud, checksum, and temporary download path
```yaml
nextcloud_download_url: https://download.nextcloud.com/server/releases/latest.tar.bz2
nextcloud_checksum_url: "sha256:{{ nextcloud_download_url }}.sha256"
nextcloud_download_path: /tmp/nextcloud.tar.bz2
```

- Nextcloud domain name
```yaml
nextcloud_domain_name: nextcloud.local
```

- Webserver document root, to extract the nextcloud folder into.
```yaml
nextcloud_www_folder: /var/www
```
Do **not** append `/nextcloud` at the end. The `nextcloud` folder will be created *inside* this directory. Here, the document root for nextcloud will be `/var/www/nextcloud`.

- SSL/HTTPS settings
```yaml
nextcloud_enable_ssl: no
nextcloud_enable_hsts: yes
```

- PHP settings
```yaml
nextcloud_php_memory_limit: 1G
nextcloud_php_opcache_strings_buffer: 16
nextcloud_php_opcache_revalidate_freq: 2
nextcloud_php_opcache_enable_jit: no
```

- Nextcloud configuration
```yaml
# Data directory for Nextcloud
nextcloud_data_directory: "/var/www/nextcloud/data"

# Trusted domains
nextcloud_trusted_domains: ["{{ nextcloud_domain_name }}"]

# Default phone region (ISO 3166-1 country codes)
nextcloud_default_phone_region:

# Install Calendar, Contacts, Mail, Nextcloud Office, Notes and Talk
nextcloud_install_recommended_apps: yes

# Install Tasks, Deck, Forms, Group folders and Recognize
nextcloud_install_suggested_apps: no

# Other additionnal apps to install
nextcloud_apps: []
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: nextcloud
      vars:
        nextcloud_database_name: nextcloud
        nextcloud_database_username: nextcloud
        nextcloud_database_password: <database_password>
        nextcloud_data_directory: /data/nextcloud
        nextcloud_php_memory_limit: 2G
        nextcloud_domain_name: "mynextcloud.example.com"
        nextcloud_default_phone_region: FR
```

License
-------

MIT
