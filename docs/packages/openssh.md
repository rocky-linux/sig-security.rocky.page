# Override package: openssh

## EL9

- Version `8.7p1-34.el9_3.security.0.1`
- Based on `8.7p1-34.el9`

### Changes summary

- Instead of linking against `libsystemd`, load it dynamically in a temporary child process to avoid polluting actual `sshd`'s address space with that library and its many dependencies (shortens `ldd sshd` output from 28 to 20 lines)

### Change log

```
* Wed Nov 22 2023 Solar Designer <solar@openwall.com> 8.7p1-34.el9_3.security.0.1
- Rebase 8.7p1-30.el9.security.0.2 on 8.7p1-34

* Sat Oct 07 2023 Solar Designer <solar@openwall.com> 8.7p1-30.el9.security.0.2
- Load libsystemd.so.0, not libsystemd.so, as the latter is only provided by
  systemd-devel

* Mon Aug 28 2023 Solar Designer <solar@openwall.com> 8.7p1-30.el9.security.0.1
- Instead of linking against libsystemd, load it dynamically in a temporary
  child process to avoid polluting actual sshd's address space with that
  library and its many dependencies (shortens "ldd sshd" from 28 to 20 lines)
```
