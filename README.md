# jora_dev_motd_banner

```text
       _                            __
      (_)____   _____ ____ _   ____/ /___  _   __
     / // __ \ / ___// __ `/  / __  // _ \| | / /
    / // /_/ // /   / /_/ /_ / /_/ //  __/| |/ /
 __/ / \____//_/    \__,_/(_)\__,_/ \___/ |___/
/___/
```

Installs a jora.dev ASCII art login banner when a user
connects via SSH.

## Requirements

- Debian/Ubuntu: `pam_motd` with the dynamic MOTD mechanism enabled
  (default on Debian/Ubuntu).
- RHEL/CentOS: version 8 or later (`pam_motd` with `/etc/motd.d` support).

## Role Variables

| Variable                    | Default                                              | Description                                 |
|------------------------------|-------------------------------------------------------|----------------------------------------------|
| `motd_banner_state`         | `present`                                            | `present` to install, `absent` to remove     |
| `motd_banner_src`           | `banner.txt`                                         | Banner text file (in `files/`), used on all OS families |
| `motd_banner_debian_dest`   | `/etc/update-motd.d/00-0header`                      | Destination path on Debian/Ubuntu            |
| `motd_banner_debian_mode`   | `'0755'`                                             | Permissions for the Debian/Ubuntu script     |
| `motd_banner_redhat_dest`   | `/etc/motd.d/00-0header`                             | Destination path on RHEL/CentOS              |
| `motd_banner_redhat_mode`   | `'0644'`                                             | Permissions for the RHEL/CentOS static file  |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - jora_dev_motd_banner
```

Override the banner text (one file for all OS families; relative paths are
looked up in the role's or playbook's `files/`):

```yaml
- hosts: all
  become: true
  roles:
    - role: jora_dev_motd_banner
      motd_banner_src: custom-banner.txt
```

Remove the banner:

```yaml
- hosts: all
  become: true
  roles:
    - role: jora_dev_motd_banner
      motd_banner_state: absent
```
