# Extra package: hardened_malloc

## EL9

- Version `hardened_malloc-12-3.el9_2.security`
- Based on upstream version `12`
- No plans to support older Rocky Linux versions due to glibc being too old

### Package summary

This package ships the "normal" and "light" configurations of the [GrapheneOS](https://grapheneos.org) [hardened_malloc](https://github.com/GrapheneOS/hardened_malloc) project. The official README.md in the upstream project documents security properties and explains the differences between the regular and light variants.

### Usage in Rocky Linux

It is strongly reccomended to read all documentation here before deploying this package on your infrastructure.

In order to support the large amount of mappings caused by guard slabs and large allocation guard regions, the `vm.max_map_count` sysctl is increased as part of package installation to `1048576` in `/etc/sysctl.d/hardened_malloc.conf`. You'll need to run `sysctl -p /etc/sysctl.d/hardened_malloc.conf` for this change to take effect without a reboot. Incidentally, [Fedora 39 made the same change](https://fedoraproject.org/wiki/Changes/IncreaseVmMaxMapCount), so it's not an exotic configuration.

The package ships 2 builds of `hardened_malloc`, the regular variant, which is located at `/usr/lib64/libhardened_malloc.so` and can be preloaded using the `hardened_malloc_preload.sh` script, and the light variant, which is located at `/usr/lib64/libhardened_malloc-light.so` and can be preloaded using the `hardened_malloc_light_preload.sh` script. The preload scripts add the relevant library to `LD_PRELOAD` and then load the desired binary, as shown in the following example: `hardened_malloc_preload.sh cat /proc/self/maps`.

Users may choose to set an OS-wide `LD_PRELOAD` with `hardened_malloc`. This can be done by adding the desired library, for example, `/usr/lib64/libhardened_malloc.so`, into your `/etc/ld.so.preload`. Be aware that for applications where `AT_SECURE` is set, this approach will not work.

It is suggested that if you wish to deploy `hardened_malloc` systemwide, that you deploy it in your `LD_PRELOAD` with the normal variant globally, and then for applications which are performance sensitive, or which fail with the normal variant, try them individually with the light variant using the preload script or by setting `LD_PRELOAD` within a systemd service namespace. If that does not resolve your issue, try disabling `hardened_malloc` by running the program in its own systemd service namespace.

### Bugs uncovered by hardened_malloc

As with all infrastructure changes, ensure you test in your staging environment extensively before deploying into production. Many packages and projects suffer from memory corruption bugs, which when running under glibc are not encountered during operation, but which `hardened_malloc` uncovers. Some applications may crash during usage, completely break, or break when running with certain configurations. Bugs in packages are typically a result of upstream project bugs, and should be reported there. In some cases these bugs are fixed in later versions in the upstream project, in which case the bug is an issue with Rocky Linux, and should be reported to Rocky Linux and its upstream distribution, so that the patch may be included.

| Package name    | Latest version tested                             | Normal variant | Light variant |
|-----------------|---------------------------------------------------|----------------|---------------|
| php             | php-8.0.30-1.el9_2.x86_64                         | Broken         | Broken        |
| php             | php-8.1.14-1.module+el9.2.0+15232+36037ab0.x86_64 | Broken         | Broken        |
| sssd            | sssd-2.8.2-3.el9_2.x86_64                         | Broken         | Broken        |

### Potential for issues with EDR

By nature of relying on `LD_PRELOAD`, if you have EDR software on your server, it may falsely send alerts when using `hardened_malloc`. If it doesn't, your EDR is probably terrible or misconfigured.

### Change log

```
* Tue Nov 14 2023 Solar Designer <solar@openwall.com> 12-3
- Package hardened_malloc_light_preload.sh
- Disable arm64 building for now (fix didn't work)

* Wed Nov  8 2023 flawedworld <flawedworld@flawed.world> 12-2
- Set CONFIG_NATIVE to false
- Mark libraries as executable (change to 755 permissions)
- Add hardened_malloc_light_preload.sh
- Fix arm64 building

* Sat Oct 28 2023 flawedworld <flawedworld@flawed.world> 12-1
- Initial packaging for hardened_malloc version 12, co-authored-by
  Scott Shinn (atomicturtle) and Solar Designer
```
