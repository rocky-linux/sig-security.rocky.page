# Extra package: lkrg

## EL9

- Version `0.9.8-1.el9_3.security`
- Based on upstream version `0.9.8`

## EL8

- Version `0.9.8-1.el8_9.security`
- Based on upstream version `0.9.8`

### Package summary

LKRG, or Linux Kernel Runtime Guard, is a kernel module that performs runtime integrity checking of the Linux kernel and detection of security vulnerability exploits against the kernel.

More information is available on the [LKRG homepage](https://lkrg.org) and in the documentation files included in the package.

### Usage in Rocky Linux

Due to EL's kABI stability and the `weak-modules` mechanism, which this package uses, the same binary package of LKRG usually works across different kernel revisions/builds within the same EL minor release (e.g., 9.3). Once there's a new minor release (e.g., 9.3 is upgraded to 9.4), we'll provide a new build of LKRG accordingly.

Installing the package does not automatically start LKRG nor enable it to start on system bootup. To start LKRG please use:

```
systemctl start lkrg
```

To enable LKRG on bootup please use:

```
systemctl enable lkrg
```

### Testing and recovery

Although the current package passed our own testing (on 9.3 and 8.9), we recommend that you only enable LKRG to start on system bootup after you've tested it for a while to ensure its compatibility with your system. If you nevertheless run into a boot time issue with LKRG later, you can disable it with the `nolkrg` kernel command-line option.

### Remote logging

LKRG includes a remote kernel message logging capability.
The corresponding userspace tools are found in the `lkrg-logger` sub-package.
Documentation is also included in there, in `/usr/share/doc/lkrg-logger/LOGGING`.

### Change log

```
* Tue Feb 27 2024 Solar Designer <solar@openwall.com> 0.9.8-1
- Update to 0.9.8
- Add logger sub-package
- Mark the sysctl configuration file config(noreplace)
- Use "sort -V" to build against the latest installed version of kernel-devel

* Wed Nov  8 2023 Solar Designer <solar@openwall.com> 0.9.7-4
- Add a couple of upstream patches, most notably to fix kINT false positives on
EL 8.8.

* Tue Oct 24 2023 Solar Designer <solar@openwall.com> 0.9.7-3
- Use weak-modules if available so that on RHEL and its rebuilds the same LKRG
  package build works across different kABI-compatible kernel revisions/builds
- Drop 32-bit x86 from ExclusiveArch since recent RHEL lacks such kernel-devel

* Thu Sep 14 2023 Solar Designer <solar@openwall.com> 0.9.7-2
- Use kernel build directory corresponding to the kernel-devel package, not to
the currently running kernel
- "BuildRequires: kernel" for the /lib/modules/* directory
- "BuildRequires: elfutils-libelf-devel" to support CONFIG_UNWINDER_ORC=y

* Thu Sep 14 2023 Solar Designer <solar@openwall.com> 0.9.7-1
- Wrote this rough RPM spec file for Red Hat'ish distros, seems to work fine on
RHEL 7, 8, 9 rebuilds, but is only reliable when there's exactly one
kernel-devel package installed at build time and it exactly matches the target
kernel version.
```
