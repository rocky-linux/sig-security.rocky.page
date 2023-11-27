# Extra package: passwdqc

## EL9

- Version `2.0.3-2.el9_2.security`
- Based on upstream version `2.0.3-2` as packaged in Fedora

## EL8

- Version `2.0.3-2.el8.security`
- Based on upstream version `2.0.3-2` as packaged in Fedora

### Package summary

`passwdqc` is a password/passphrase strength checking and policy enforcement toolset, including a PAM module (`pam_passwdqc`), command-line programs (`pwqcheck`, `pwqfilter`, and `pwqgen`), and a library (`libpasswdqc`).

More information is available on the [passwdqc homepage](https://www.openwall.com/passwdqc/) and in the documentation files (man pages and a README) included in the sub-packages below.

### Usage in Rocky Linux

There are 5 sub-packages:

#### pam_passwdqc

`pam_passwdqc` is a PAM module that is normally invoked on password changes by programs such as `passwd(1)`. It is capable of checking password or passphrase strength, enforcing a policy, and offering randomly-generated passphrases, with all of these features being optional and easily (re-)configurable.

Merely installing this sub-package does not yet configure the system to use the PAM module. To do so, please edit PAM configuration files e.g. like [shown here](https://github.com/openwall/passwdqc/issues/19#issuecomment-1140262371).

#### passwdqc-utils

`pwqcheck` and `pwqgen` are standalone password/passphrase strength checking and random passphrase generator programs, respectively, which are usable from scripts.

The `pwqfilter` program searches, creates, or updates binary passphrase filter files, which can also be used with `pwqcheck` and `pam_passwdqc`. This can be used for checking of user-provided passwords against existing data breaches, which is recommended in the current NIST guidance, specifically in publication 800-63B sections 5.1.1.2 and A.3. Paid pre-generated filter files are available from Openwall at the project homepage above, but with this tool you can also generate your own.

#### libpasswdqc

`libpasswdqc` is the underlying library, which may also be used from third-party programs.

#### libpasswdqc-devel

This package contains development files needed for building passwdqc-aware applications, as well as documentation (man pages) for developing such applications.

#### passwdqc

`passwdqc` is a meta sub-package that installs (via dependencies) the actual sub-packages above, except for `libpasswdqc-devel`.
