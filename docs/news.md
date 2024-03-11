# News

These are what we consider significant SIG/Security news items, not an exhaustive list of package updates and wiki edits.

## March 11, 2024

[openssh](packages/openssh.md) rebased on upstream EL 8.7p1-34.3 with fixes for CVE-2023-48795 (Terrapin attack) and CVE-2023-51385, now building it without Kerberos support (further shortens `ldd sshd` from 20 to 13 lines, down from 28 lines in upstream EL).

## February 28, 2024

[lkrg](packages/lkrg.md) updated to version 0.9.8, which adds a remote kernel message logging capability.

## January 31, 2024

Further EL9 [glibc](packages/glibc.md) security hardening in response to the [recent](https://www.openwall.com/lists/oss-security/2024/01/30/6) [findings](https://www.openwall.com/lists/oss-security/2024/01/30/7) by Qualys.

## January 3, 2024

[control](packages/control.md) `0.8.0-7` can now manage two SUID root PAM helper programs `unix_chkpwd` and `pam_timestamp_check`.

## December 27, 2023

[control](packages/control.md) `0.8.0-5` can now manage user password hashing scheme and password policy in use by PAM-aware programs.

## December 18, 2023

This SIG/Security News wiki page has been created, retroactively identifying and listing selected news items so far.

[control](packages/control.md) `0.8.0-4` can now manage 3 privileged programs from `util-linux` (and `util-linux-core`): `mount`, `umount` (one "facility" for both), and `write`. Its wiki page has been reworked.

## December 14, 2023

[control](packages/control.md) wiki page added, documenting the new package.

`control` provides a common interface to register and control (what it calls) system facilities.
This is intended primarily for facilities that can potentially be dangerous to system security, to let you enable, disable, or configure each facility.
A typical facility is a SUID/SGID/setcap program or a configuration setting of a service.

Included initially are facility specifications corresponding to the `shadow-utils` package. Currently, these allow to `control` access to 5 privileged programs - 3 of them (`chage`, `gpasswd`, and `newgrp`) are by default SUID root and 2 (`newuidmap` and `newgidmap`) are `cap_setuid=ep`.

## November 25, 2023

Everything we had so far has been updated for EL 9.3 and 8.9, including our hardened EL9 [glibc](packages/glibc.md) and [openssh](packages/openssh.md) packages rebased on 9.3's and [lkrg](packages/lkrg.md) rebuilt for 9.3's and 8.9's kernels, along with re-testing and wiki edits.

The `rocky-release-security` package containing our repository configuration has been made (a while earlier) easier to use on EL distros other than Rocky Linux, and we've now updated the wiki accordingly.

## November 16 to 19, 2023

[microcode_ctl](packages/microcode_ctl.md) also for EL8, providing 8.9's Intel CPU microcode to fix [CVE-2023-23583](issues/CVE-2023-23583.md) a few days before general availability of our own 8.9 release as a whole.

## November 16, 2023

Wiki pages [lkrg](packages/lkrg.md) and [passwdqc](packages/passwdqc.md) have been created. We had these extra packages for a while, but previously only had wiki pages for override packages (referring solely to upstream homepages for the extra packages).

## November 15, 2023

We've started maintaining wiki pages for selected high profile security issues, initially for glibc [CVE-2023-4911](CVE-2023-4911.md) and Intel CPU microcode [CVE-2023-23583](issues/CVE-2023-23583.md).

[microcode_ctl](packages/microcode_ctl.md) for EL9, providing latest Intel CPU microcode to fix [CVE-2023-23583](issues/CVE-2023-23583.md) ahead of availability of a rebuilt new upstream package.

## October 31 to November 15, 2023

[hardened_malloc](packages/hardened_malloc.md) package - a security-focused memory allocator providing the `malloc(3)` API, and a script to preload it into existing program binaries. Its documentation on the wiki.

## October 13, 2023

We've started maintaining per-package wiki pages, initially for the override packages of [glibc](packages/glibc.md) and [openssh](packages/openssh.md).

We've added instructions for installation of Rocky Linux SIG/Security repository on other EL distros (non-Rocky).

## October 3, 2023

Initial wiki content documenting what we had so far, which included override packages of [glibc](packages/glibc.md) and [openssh](packages/openssh.md) and extra packages of [lkrg](packages/lkrg.md) and [passwdqc](packages/passwdqc.md) (even though these per-package wiki pages did not exist yet, so we instead had summaries and external links on the front page only), the repository package, [source code repositories](https://git.rockylinux.org/sig/security/src), and [Mattermost channel](https://chat.rockylinux.org/rocky-linux/channels/security).
