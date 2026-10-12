# Night SELinux Guard

Night SELinux Guard replaces the Manager-facing `selinux_hide` feature with the
canonical `night_selinux_guard` identity. Feature ID 4 is retained for kernel
ABI compatibility, and the old command name remains an input-only alias so an
existing saved configuration or module does not break during an upgrade.

## Security boundary

- The real SELinux enforcing state is not changed.
- SELinux audit generation is not disabled or cleared.
- The compatibility view is limited to the existing unprivileged app-UID path.
- System and root callers continue to use the real SELinux interfaces.
- Enable and disable operations report the actual runtime state. A failed patch
  or rollback is returned as an error instead of being displayed as successful.

## User interface and persistence

The Manager exposes one switch named **Night SELinux Guard**. It stores the
canonical `night_selinux_guard` name through ksud and re-applies feature ID 4
after reboot. There is no second SELinux-hiding implementation or duplicate
switch.

## Compatibility

The following commands address the same feature:

```text
ksud feature get night_selinux_guard
ksud feature get selinux_hide
ksud feature get 4
```

New configuration should always use `night_selinux_guard`.
