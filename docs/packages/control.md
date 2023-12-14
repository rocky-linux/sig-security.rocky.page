# Extra package: control

## EL9

- Version `0.8.0-2.el9_3.security`

### Package summary

`control` provides a common interface to register and control (what it calls) system facilities.
This is intended primarily for facilities that can potentially be dangerous to system security, to let you enable, disable, or configure each facility.
A typical facility is a SUID/SGID/setcap program or a configuration setting of a service.

`control` originates in Owl and is actively maintained in ALT Linux.

### Usage in Rocky Linux

While the original `control` package in Owl and ALT Linux merely provides the common interface mentioned above for other packages to register their facilities with (and many packages in those distros do), it's been adapted in Rocky Linux to provide its own sub-packages with facility specifications and RPM trigger scripts for other packages coming from EL. This way, we can `control` those facilities and have custom settings persist (be automatically saved and restored) over package upgrades without us having to maintain forks of those other packages.

Initially, there are 2 sub-packages:

#### control

The main package providing the common interface, but no facilities of its own.
Please refer to `control(8)` man page for command-line usage syntax.

#### control-shadow

Facility files corresponding to the `shadow-utils` package. Currently, these allow to `control` access to 5 privileged programs (3 of them are by default SUID root and 2 `cap_setuid=ep`, thus posing risk to system security in case of vulnerabilities in them).

```
# control
chage           public          (public restricted)
gpasswd         public          (public wheelonly restricted)
newgidmap       public          (public wheelonly restricted)
newgrp          public          (public wheelonly restricted)
newuidmap       public          (public wheelonly restricted)
```
