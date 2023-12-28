# Extra package: control

## EL9

- Version `0.8.0-5.el9_3.security`

### Package summary

`control` provides a common interface to register and control (what it calls) system facilities.
This is intended primarily for facilities that can potentially be dangerous to system security, to let you enable, disable, or configure each facility.
A typical facility is a configuration setting of a service or a SUID/SGID/setcap program, or a closely related group of such settings and/or programs that are managed together.
We manage permissions on SUID/SGID/setcap programs because those programs pose risk to system security in case of vulnerabilities in them or in library code they use.

`control` originates in Owl and is actively maintained in ALT Linux.

### Usage in Rocky Linux

While the original `control` package in Owl and ALT Linux merely provides the common interface mentioned above for other packages to register their facilities with (and many packages in those distros do), it's been adapted in Rocky Linux to provide its own sub-packages with facility specifications and RPM trigger scripts for other packages coming from EL. This way, we can `control` those facilities and have custom settings persist (be automatically saved and restored) over package upgrades without us having to maintain forks of those other packages.

The available facilities, their current settings, and lists of possible settings can be queried by running the `control` command without parameters. With all currently available sub-packages installed and upstream default settings, its output is:

```
chage           public          (public restricted)
gpasswd         public          (public wheelonly restricted)
mount           public          (public wheelonly unprivileged restricted)
newgidmap       public          (public wheelonly restricted)
newgrp          public          (public wheelonly restricted)
newuidmap       public          (public wheelonly restricted)
password-hash   sha512crypt     (sha512crypt yescrypt)
password-policy pwquality       (pwquality passwdqc)
write           public          (public restricted)
```

With maximum security hardening, it changes to:

```
chage           restricted      (public restricted)
gpasswd         restricted      (public wheelonly restricted)
mount           restricted      (public wheelonly unprivileged restricted)
newgidmap       restricted      (public wheelonly restricted)
newgrp          restricted      (public wheelonly restricted)
newuidmap       restricted      (public wheelonly restricted)
password-hash   yescrypt        (sha512crypt yescrypt)
password-policy passwdqc        (pwquality passwdqc)
write           restricted      (public restricted)
```

The default settings (typically `public`) correspond to EL packages' defaults (and are typically the most relaxed security-wise).

Please refer to `control(8)` man page for command-line usage syntax.

### Sub-packages

Currently, there are 3 sub-packages:

#### control

The main package providing the common interface, but no facilities of its own.

#### control-shadow-utils

Facility specifications corresponding to the `shadow-utils` package. Currently, these allow to `control` access to 5 privileged programs - 3 of them (`chage`, `gpasswd`, and `newgrp`) are by default SUID root and 2 (`newuidmap` and `newgidmap`) are `cap_setuid=ep`.

#### control-util-linux

Facility specifications corresponding to the `util-linux` and `util-linux-core` packages. Currently, these allow to `control` access to 3 privileged programs - 2 of them (`mount` and `umount`) are by default SUID root and 1 (`write`) SGID `tty`.

#### control-pam

Facility specifications corresponding to the `pam` package. Currently, these allow to `control` user password hashing scheme and password policy in use by PAM-aware programs.

### Change log

```
* Wed Dec 27 2023 Solar Designer <solar@openwall.com> 0.8.0-5
- Install control(8) mode 755 since some of its features work as non-root
- Add sub-package with facilities and triggers for pam password hashing and
  password policy

* Mon Dec 18 2023 Solar Designer <solar@openwall.com> 0.8.0-4
- Add sub-package with facilities and triggers for util-linux

* Mon Dec 18 2023 Solar Designer <solar@openwall.com> 0.8.0-3
- Rename the shadow sub-package to shadow-utils
- Rename the source files not to differentiate them by sub-package
- Add "Requires: shadow-utils" in the shadow-utils sub-package

* Wed Dec 13 2023 Solar Designer <solar@openwall.com> 0.8.0-2
- In addition to Requires(pre), also use Requires in the sub-package
- In %%triggerprein_control, pre-check that the facility exists
- Use (renamed) copies of the trigger macros within this spec file

* Wed Dec 13 2023 Solar Designer <solar@openwall.com> 0.8.0-1
- Add macros for use in RPM triggers
- Add sub-package with facilities and triggers for shadow-utils

* Wed Dec  6 2023 Solar Designer <solar@openwall.com> 0.8.0-0
- Initial packaging for EL based on ALT Linux and Owl packages
```
