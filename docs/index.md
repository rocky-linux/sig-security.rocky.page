# SIG/Security Wiki

The Security SIG repositories provide extra security-related packages and security-hardened override packages (replacing those from the main distribution) for Rocky Linux and other Enterprise Linux (EL) distributions.

## Responsibilities

Developing and maintaining various security related packages that are not in upstream EL. Identifying, developing, and maintaining security hardening changes relative to upstream EL packages. Occasionally including/backporting additional security fixes that are not yet in upstream EL packages. Contributing to the respective upstreams where practical.

## Repo Installation

### On Rocky Linux

```
dnf install rocky-release-security
```

### On another compatible EL distro

Download the release package containing our repository configuration file and package signing public key. Use the version that corresponds to the major version of your EL distro.

- [rocky-release-security-9](https://download.rockylinux.org/pub/rocky/9/extras/x86_64/os/Packages/r/rocky-release-security-9-3.el9.noarch.rpm)
- [rocky-release-security-8](https://download.rockylinux.org/pub/rocky/8/extras/x86_64/os/Packages/r/rocky-release-security-8-3.el8.noarch.rpm)

Verify the package file's SHA-256 digest with `sha256sum`. The currently expected digests are:

```
0d0cfcb16379b4c374b45a7a4ec86894f5bbdd977103cc5544be0f6fc2581a2a  rocky-release-security-9-3.el9.noarch.rpm
8dc7912f0ab55dff4cb2b1dc9262c22aa89d911cdb680d33213737597d865006  rocky-release-security-8-3.el8.noarch.rpm
```

This isn't as secure as checking the package signature would be _if_ you previously had our package signing public key, but on another distro you probably don't have that yet, so checking the digest against its copy obtained from this separate website is a best-effort measure.

## Packages

### Extra packages (for EL8 and EL9)

- [lkrg](packages/lkrg.md) (Linux Kernel Runtime Guard)
- [passwdqc](packages/passwdqc.md) (password/passphrase strength checking and policy enforcement)

### Extra packages (currently only for EL9)

- [control](packages/control.md) (a common interface to register and control security-relevant system facilities)
- [hardened_malloc](packages/hardened_malloc.md) (security-focused memory allocator providing the malloc API, and a script to preload it into existing program binaries)

### Override packages (for EL8 and EL9)

- [microcode_ctl](packages/microcode_ctl.md) (updates Intel CPU microcode to fix [CVE-2023-23583](issues/CVE-2023-23583.md))

### Override packages (currently only for EL9)

- [glibc](packages/glibc.md) (adds many security-hardening changes originating from Owl and ALT Linux on top of EL package)
- [openssh](packages/openssh.md) (fewer shared libraries exposed in sshd processes while otherwise fully matching EL package's functionality)

The changes are described in more detail on the per-package wiki pages linked above, as well as in the package changelogs.
More packages/changes are planned, including override packages also for EL8.

## Source code

Just like for other Rocky Linux SIGs, the source trees for Security SIG packages are maintained in [per-package git repositories](https://git.rockylinux.org/sig/security/src). Each repository contains branches `r8` and/or `r9` corresponding to target EL version.

## Contributing

If anyone else wants to join this effort - in any capacity including development, maintenance, testing, documentation, user support, spreading the word, or something else - please join the Mattermost channel below and let us know!

We also welcome well-reasoned suggestions/feedback/preferences on direction we should take (e.g., only making changes on top of EL's vs. offering newer upstream versions), what else to package, and what other changes to include.

## Meetings / Communications

We hang out in our [Security Mattermost channel](https://chat.rockylinux.org/rocky-linux/channels/security).

## Members

Some of the people active with setting up this SIG so far:

| Name            | Mattermost Name |
|-----------------|-----------------|
|                 | @flawedworld    |
| Fredrik Nyström | @nscfreny       |
| Louis Abel      | @label          |
| Mustafa         | @mustafa        |
| Neil Hanlon     | @neil           |
| Scott Shinn     | @atomicturtle   |
| Solar Designer  | @solardiz       |
