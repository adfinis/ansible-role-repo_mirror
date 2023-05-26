# ROLE REPO MIRROR

[![image](https://img.shields.io/github/license/adfinis-sygroup/ansible-role-repo_mirror.svg?style=flat-square)](https://github.com/adfinis-sygroup/ansible-role-repo_mirror/blob/master/LICENSE)

[![image](https://img.shields.io/travis/adfinis-sygroup/ansible-role-repo_mirror.svg?style=flat-square)](https://github.com/adfinis-sygroup/ansible-role-repo_mirror)

[![image](https://img.shields.io/badge/galaxy-adfinis--sygroup.repo_mirror-660198.svg?style=flat-square)](https://galaxy.ansible.com/adfinis-sygroup/repo_mirror)

Ansible role that helps deploying a package mirror

## Requirements

-   A debian system with bullseye is required
-   systemd as init system is required
-   Before you use this role, create a storage pool with something like
    ZFS and mount it at the location where the mirrored repositories
    would appear.

## Role Variables

```yaml
# vars/Debian.yml
---

# script dependencies to be installed
repo_mirror_packages:
  - rsync
  - wget
  - logrotate
  - git
  - systemd
```

```yaml
---

# vars/Debian.yml

# The default user mirrors will use
repo_mirror_user: mirror

# The default group mirrors will use
repo_mirror_group: mirror

# The mirror base path
repo_mirror_base_path: /var/www/mirror

# The default log path
repo_mirror_log_path: /var/log/mirror

# The default tmp path (files which are currently downloaded)
repo_mirror_tmp_path: /var/www/mirror/tmp

# This is the default datetime format (2017/10/11 22:23:42 CEST)
repo_mirror_datetime_format: "+%Y/%m/%d %T %Z"

# The default bandwith limit for syncing from remote
repo_mirror_bwlimit: 30MiB

# The default rsync timeout in seconds
repo_mirror_rsync_timeout: 30

# the default max runtime for a sync job
_default_systemd_unit_max_runtime_sec: 43200  # 12 hours

# the default enabled state of a systemd timer unit
_default_systemd_timer_enabled: true

# the default unit state of a systemd timer unit
_default_systemd_timer_unit_state: 'started'

# the default unit state of a systemd service unit
_default_systemd_service_unit_state: 'stopped'

# The FQDN of the mirror
repo_mirror_fqdn: 'mirror.example.com'

# Deploy the fedora mirror report script
repo_mirror_fedora_report: false
repo_mirror_fedora_report_name: '<name>'
repo_mirror_fedora_report_pass: '<password>'

# A list of fedora projects to report. Default is an empty list.
repo_mirror_fedora_reports: []

# .. code-block:: YAML
#
#   repo_mirror_fedora_reports:
#     - name: 'Fedora EPEL'
#       enabled: false
#       path: '/var/www/mirror/epel'
#     - name: 'Fedora Linux'
#       enabled: False
#       path: '/var/www/mirror/fedora'

# A list of repositories. Default is an empty list.
# Below are some examples how to define a repository to mirror
repo_mirror_repos: []

# .. code-block:: YAML
#
#   repo_mirror_repos:
#     - name: alpine
#       type: rsync_single
#       source_repo: rsync://rsync.alpinelinux.org/alpine/
#       systemd_timer_calendar: "*-*-* 0/2:23:00"
#       systemd_timer_disabled: true # does not enable the timer (e.g. will not be started on boot), default false
#       systemd_unit_max_runtime_sec: 600 # 10 minutes, default 43200
#
#     - name: archlinux
#       source_repo: rsync://mirror.23media.de/archlinux
#       type: rsync_single
#       systemd_timer_calendar: "*-*-* *:0/10:00"
#
#     - name: debian
#       type: rsync_debian
#       source_repo: 'ftp.ch.debian.org::debian'
#       systemd_timer_calendar: "*-*-* 0/2:01:00"
#       excludes:
#       - alpha
#       - arm
#       - arm64
#       - armel
#       - armhf
#       - hppa
#       - hurd-i386
#       - ia64
#       - kfreebsd-amd64
#       - kfreebsd-i386
#       - m68k
#       - mipsel
#       - mips64el
#       - mips
#       - powerpc
#       - ppc64el
#       - s390
#       - s390x
#       - sh
#       - sparc
#
#     - name: debian-security
#       type: rsync_single
#       source_repo: security.debian.org::debian-security
#       systemd_timer_calendar: "*-*-* 0/2:13:00"
#
#     - name: epel
#       type: rsync_single
#       source_repo: rsync://dl.fedoraproject.org/fedora-epel
#       additional_report: '/usr/local/bin/report_mirror -c /etc/mirror/fedora_report.conf'
#       systemd_timer_calendar: "*-*-* *:58:00"
#
#     - name: centos
#       type: rsync_single
#       source_repo: eu-msync.centos.org::CentOS
#       rsync_timeout: 300 # Optional, if for example .ISO files time out
#       systemd_timer_calendar: "*-*-* *:13:00"
#
#     - name: dotdeb
#       type: rsync_single
#       source_repo: packages.dotdeb.org::packages
#       systemd_timer_calendar: "*-*-* *:47:00"
#
#     - name: nodejs
#       type: wget
#       source_repo: 'https://deb.nodesource.com/node_7.x/'
#       remotegpgkey: 'https://deb.nodesource.com/gpgkey/nodesource.gpg.key'
#       bwlimit: 20000 # Optional, overwrite default
#       systemd_timer_calendar: "*-*-* 0/2:24:00"
#
#     - name: opensuse
#       type: rsync_single
#       source_repo: stage.opensuse.org::opensuse-hotstuff-640gb
#       systemd_timer_calendar: "*-*-* *:07:00"
#
#     - name: ubuntu
#       type: rsync_ubuntu
#       source_repo: rsync://ch.rsync.archive.ubuntu.com/ubuntu
#       systemd_timer_calendar: "*-*-* 0/2:41:00"
```

## Dependencies

Please see the [meta/main.yml](https://github.com/adfinis/ansible-role-repo_mirror/blob/master/meta/main.yml) file for requirements for
this role and the [molecule_requirements.yml](https://github.com/adfinis/ansible-role-repo_mirror/blob/master/molecule_requirements.yml) file for the
molecule requirements.

## Example Playbook

You can check the molecule default scenario for an example playbook.

## License

[GPL-3.0](https://github.com/adfinis/ansible-role-repo_mirror/blob/master/LICENSE)

## Author Information

repo_mirror role was written by:

-   Adfinis AG | [Website](https://www.adfinis.com/) \|
    [Twitter](https://twitter.com/adfinissygroup) \|
    [GitHub](https://github.com/adfinis-sygroup)
