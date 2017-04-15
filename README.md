# Php-FPM Ansible role

This is an ansible role which sets up a php-fpm instance and configures the pools.


## Requirements

This role needs systemd and an apt based package manager.


## Role Variables

To see all vars possible for php-fpm see 
[php-fpm config page](https://secure.php.net/manual/en/install.fpm.configuration.php)


To see all vars possible for php.ini see
[php.ini page](https://secure.php.net/manual/de/ini.list.php)

For a domain

| Name                      | Required                 | Description       | 
|---------------------------|:------------------------:|---------------|
| `name`          | :heavy_check_mark:       | Name of the pool         |
| `listen`          | :heavy_check_mark:         | The address on which to accept FastCGI requests. Valid syntaxes are: 'ip.add.re.ss:port', 'port', '/path/to/unix/socket'. This option is mandatory for each pool.  |
| `user`          | :heavy_check_mark:         | Unix user of FPM processes. This option is mandatory.|
| `pm`          | :heavy_check_mark:           | Choose how the process manager will control the number of child processes. Possible values: static, ondemand, dynamic. This option is mandatory. |
| `pm.max_children`          | :heavy_check_mark:         | The number of child processes to be created when pm is set to static and the maximum number of child processes to be created when pm is set to dynamic. This option is mandatory. |




## Example Playbook

### Vars

```yml
pools:
  - name: fpm-host
    listen: /path/to/unix/socket
    user: www-data
    pm: static
    pm.max_children: 20
    pm.start_servers: 20
    processes_priority: -19
php_ini_values:
  apc.enabled:
    - 1
  extension:
    - php_mysqli.dll
    - php_ldap.dll
log_level: error
```


### Result

A running php-fpm instance


## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

 * [Fritz Otlinghaus (Scriptkiddi)](https://github.com/Scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
