Ansible role configure_php_ini
=========

Ansible role to configure php.ini file of our Apache server in acordance to the listed on php_ini_parameters_and_values

Requirements
------------

Ansible >= 2.3

Role Variables
--------------

By default, PHP version is set according to default version of the distribution: 7.0 in debian stretch, 7.0 in debian buster.

If you use a custom version of PHP, you can force it with the variable `php_ini_php_version`. 

Full paths to `cli/php.ini` and `apache2/php.ini` files are set to default ones, acccording to PHP version. But you can also force them defining the variables `cli_php_ini_path` and/or `apache_php_ini_path`.

PHP configuration parameters themselves, for CLI PHP and/or Apache PHP are set with the following structures (choice of parameters subset and values are, of course, exampes): 

```yaml

# List of CLI PHP parameters to configure
cli_php_ini_parameters_and_values:
- parameter: post_max_size
  value: 1G
- parameter: upload_max_filesize
  value: 1G
- parameter: max_execution_time
  value: 90
- parameter: max_input_time
  value: 90
- parameter: memory_limit
  value: 256M
- parameter: date.timezone
  value: '"America/Montevideo"'

# List of APACHE PHP parameters to configure
apache_php_ini_parameters_and_values:
- parameter: post_max_size
  value: 256M
- parameter: upload_max_filesize
  value: 256M
- parameter: date.timezone
  value: '"America/Montevideo"'
```

Notice that string values must be double quoted to remain quoted in `php.ini` file.  

Dependencies
------------

No dependences

Example Playbook
----------------

```yaml
- hosts: servers_lamp
  roles:
  - role: configure_php_ini
    cli_php_ini_parameters_and_values:
    - parameter: max_execution_time
      value: 90
    - parameter: max_input_time
      value: 90
    apache_php_ini_parameters_and_values:
    - parameter: post_max_size
      value: 256M
    - parameter: upload_max_filesize
      value: 256M

```

License
-------

(c) Universidad de la República (UdelaR), Red de Unidades Informáticas de la UdelaR en el Interior.
licenced under GPL-v3

Author Information
------------------

[@santiagomr](https://github.com/santiagomr)
[@UdelaRInterior](https://github.com/UdelaRInterior)
https://proyectos.interior.edu.uy/
