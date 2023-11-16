# Override package: microcode_ctl

## EL9

- Version `4:20231114-1.el9_2.security`
- Based on `4:20230808-2.el9`

This is our custom revision of a post-9.2 EL9 package. We use Intel's latest released microcode.

## EL8

- Version `4:20230808-2.20231009.1.el8.security`
- Based on `4:20230808-2.20231009.1.el8`

This is a rebuild of the 8.9 package as-is to make it available for 8.8. It uses Intel's fixed microcode revision that was provided to distros privately in preparation for the coordinated disclosure.

### Changes summary

- Update Intel CPU microcode to fix [CVE-2023-23583](../issues/CVE-2023-23583.md), temporarily dropping most documentation patches

### Change log

For EL9:

```
* Tue Nov 14 2023 Solar Designer <solar@openwall.com> - 4:20231114-1
- Update Intel CPU microcode to microcode-20231114 (fixes CVE-2023-23583),
  temporarily dropping most documentation patches
```
