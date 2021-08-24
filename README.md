ansible-role-grub
=================

Manages grub config on RHEL/Centos.

Requirements
------------

This is a standalone role.

Role Variables
--------------

Additional kernel parameters can be passed using the following two lists.
```yaml
# additional cmdline arguments
grub_cmdline_linux_list: []

# additional cmdline default arguments
grub_cmdline_linux_default_list: []
```

Additional tty instances can be added to the follwing list. 
For example a serial connection which has its own set of variables.
```yaml
# start grub and linux on these consoles
grub_consoles:
  - tty0
  - 'ttyS0,{{ grub_serial.speed }}'

# grub serial command settings
grub_serial:
  speed: 115200
  unit: 0
  word: 8
  parity: 0
  stop: 1
```

Dependencies
------------

No hard dependencies.

Example Playbook
----------------

An example playbook which installs and configures grub with kernel parameters.
```yaml
---

- name: grub test play
  hosts: all
  become: true
  vars:
    grub_cmdline_linux_list:
      - crashkernel=auto
      - rd.lvm.lv=vg01/root
      - rhgb
      - quiet
      - boot=a27cca18-a888-4b0e-9066-986d22036054
      - vsyscall=none
      - slub_debug=P
      - page_poison=1
      - audit_backlog_limit=8192
      - audit=1
  roles:
    - grub
```

License
-------

GPLv3

Author Information
------------------

Aaron (aaron@0x29a.ch)
