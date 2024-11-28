Ansible Role: Unattended Upgrades
=========

An ansible role for configuring unattended package upgrades on debian like systems

Requirements
------------

none

Role Variables
--------------

|Variable|Default|Description|
|---|---|---|
|unattended_upgrades_origins_distro_recommended|false|include (non-critical) distro recommended updates|
|unattended_upgrades_origins_distro_proposed|false|include distro proposed updates|
|unattended_upgrades_origins_distro_backports|false|include distro bakcported updates|
|unattended_upgrades_origins_additional|[]|a list of any additional origins that you want to be included|
|unattended_upgrades_handle_conffile_prompt|false|configures apt to automatically handle any changes to packaged config files|
|unattended_upgrades_auto_reboot|false|reboot host if required (e.g. for kernel upgrades)|
|unattended_upgrades_auto_reboot_time|now|when to reboot (e.g. 02:00, or +5m) ([shutdown command format](https://linux.die.net/man/8/shutdown))|
|unattended_upgrades_upgrade_timer_oncalendar|*undefined*|when to run unattended upgrades ([systemd calendar event format](https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html#Calendar%20Events))|


Dependencies
------------

none

Example Playbook
----------------

configure servers to automatically upgrade packages on the first Sunday of the month, including (non-critical) recommended distro updates, to automatically handle any package conf file changes, and to reboot the server as necessary

```
  - hosts: servers
      
    vars:
      unattended_upgrades_upgrade_timer_oncalendar: 'Sun *-*-01..07 06:00'
      unattended_upgrades_origins_distro_recommended: true
      unattended_upgrades_handle_conffile_prompt: true
      unattended_upgrades_auto_reboot: true
  
    roles:
      - dataraven.unattended_upgrades
```

License
-------

BSD 3-Clause License

Author Information
------------------

Ben Albon - ben@dataraven.co.uk
