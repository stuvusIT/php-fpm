# Php-FPM Ansible role

This is an ansible role which sets up a php-fpm instance and configures the pools.


## Requirements

This role needs systemd and an apt based package manager.


## Role Variables

To see all vars possible for php-fpm see 
[php-fpm config page](https://secure.php.net/manual/en/install.fpm.configuration.php). To use them prefix them with php_fpm_ (but not the pool variables)


To see all vars possible for php.ini see
[php.ini page](https://secure.php.net/manual/de/ini.list.php)
To pass those vars to ansible you use the list
`php_fpm_php_ini_values` the syntax for this is as follows
```
php_fpm_php_ini_values:
  - section: SECTION NAME
    option: OPTION NAME
    value: VALUE
```
| Name                      | Required                 | Description       | 
|---------------------------|:------------------------:|---------------|
| `section`          | :heavy_check_mark:       | Name from the php ini file section where the variable is supposed to live.        |
| `option`          | :heavy_check_mark:         | The actuall variable name |
| `value`          | :heavy_check_mark:         | The value that the option should have|

For a domain

| Name                      | Required                 | Description       | 
|---------------------------|:------------------------:|---------------|
| `name`          | :heavy_check_mark:       | Name of the pool         |
| `listen`          | :heavy_check_mark:         | The address on which to accept FastCGI requests. Valid syntaxes are: 'ip.add.re.ss:port', 'port', '/path/to/unix/socket'. This option is mandatory for each pool.  |
| `user`          | :heavy_check_mark:         | Unix user of FPM processes. This option is mandatory.|
| `pm`          | :heavy_check_mark:           | Choose how the process manager will control the number of child processes. Possible values: static, ondemand, dynamic. This option is mandatory. |
| `pm.max_children`          | :heavy_multiplication_x:         | The number of child processes to be created when pm is set to static and the maximum number of child processes to be created when pm is set to dynamic. This option is mandatory if pm is set to dynamic or static. |




## Example Playbook

### Vars

```yml
php_fpm_pools:
  - name: fpm-host
    listen: /path/to/unix/socket
    user: www-data
    pm: static
    pm_max_children: 20
    pm_start_servers: 20
    processes_priority: -19
php_fpm_php_ini_values:
  - section: APC
    option: apc.enabled
    value: 1
  - section: PHP
    option: extension
    value: php_mysqli
  - section: PHP
    option: extension
    value: php_ldap
php_fpm_log_level: error
```

php_ini_values are all treated as a list since ansible can not differniate between types
### Result

A running php-fpm instance


## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

 * [Fritz Otlinghaus (Scriptkiddi)](https://github.com/Scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
