# Role Name

This is an ansible role which sets up a php-fpm instance and configures the pools.


## Requirements

This role needs systemd and an apt based package manager.


## Role Variables

To see all vars possible for php-fpm see 
[php-fpm config page](https://secure.php.net/manual/en/install.fpm.configuration.php)


To see all vars possible for php.ini see
[php.ini page](https://secure.php.net/manual/de/ini.list.php)

```yml
fpm_conf.log_level: error
php_ini_values:
  apc.enabled: 1

```



## Example Playbook

### Vars

```yml
pools:
  - name: fpm-host
    listen: /path/to/unix/socket
    user: www-data
    pm: static
    pm.max_children = 20
php_ini_values:
  apc.enabled: 1
fpm_conf:
  log_level: error
```


### Result

A running php-fpm instance


## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

 * [Fritz Otlinghaus (Scriptkiddi)](https://github.com/Scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
