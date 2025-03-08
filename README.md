# Ansible role: test

|Source|Version|CI|License|Code style|
|------|-------|-------|-------|-------|
|[![Source Code](https://img.shields.io/badge/source-github-blue.svg)](https://github.com/grzegorzfranus/test)|[![Version](https://img.shields.io/github/v/release/grzegorzfranus/test)](https://github.com/grzegorzfranus/test/releases)|[![tests](https://github.com/grzegorzfranus/test/actions/workflows/ci.yml/badge.svg)](https://github.com/grzegorzfranus/test/actions)|[![Repository License](https://img.shields.io/badge/license-apache2.0-brightgreen.svg)](LICENSE)|[![Python Black Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/python/black)|

## Overview

Ansible role to install and configure chrony NTP client.

Chronyd is a daemon for synchronisation of the system clock.

## Main actions

* Install Chrony package.
* Configure Chrony service.
* Set up logrotate (optional).
* Upgrade Chrony package (optional).

## Version

- `v1.0.0` - initial version  

## Requirements

### Supported operating systems

| OS Family | Version | Status |
|-----------|---------|---------|
| Ubuntu | 22.04 (Jammy) | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |
| Debian | 12 (Bookworm) | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |
| Rocky Linux | 9 | ![✓](https://img.shields.io/badge/✓-brightgreen.svg) |

### Root access

List of officially supported operating systems:


### Ansible version

Ansible >= 2.15

### Python version

Python >= 3.11

### Setup module
The role uses facts gathered by Ansible on the remote host. If you disable the Setup module in your playbook, the role will not work properly.

### Root access
This role requires root access for some tasks. Make sure that you are using a user with root privileges.

## Role Variables

### Main variables

* `chrony_role_action` - Specific role action.
* `chrony_service_enabled` - Enables or disables Chrony at system startup.
* `chrony_configure_logrotate` - Enables or disables logrotate for Chrony service.
* `chrony_run_test` - Run task to check Chrony synchronize status.

### Chrony Configuration

* `chrony_ntp_source_mode` - pool or server
* `chrony_ntp_servers` - A list of NTP servers that Chrony will use to synchronize the system clock. Each server can be configured with specific options like iburst for faster initial synchronization.
* `chrony_rtcsync_enable` - Enables or disables synchronization of the system clock to the Real-Time Clock (RTC) using the kernel's 11-minute mode, ensuring periodic updates.
* `chrony_maxdistance` - Sets the maximum acceptable root distance for a source to be considered valid for synchronization. Helps filter out unreliable NTP sources.
* `chrony_ntsdumpdir` - Specifies the directory where Chrony will store dumps of non-volatile memory timestamps, which help in maintaining accurate time after a reboot.
* `chrony_num_minsources` - Defines the minimum number of NTP sources required before Chrony selects and synchronizes with a time source. Ensures accuracy by preventing synchronization with too few sources.
* `chrony_maxupdateskew` - Limits the allowed skew (offset fluctuation) of an NTP source before it is considered unreliable. Helps maintain time stability.
* `chrony_makestep` - Specifies the conditions under which Chrony will make a sudden step correction to the clock instead of gradually adjusting it. Commonly used for large time offsets.
* `chrony_logchange` - Sets the threshold for logging significant time changes in system synchronization. Helps in monitoring and diagnosing time-related anomalies.
* `chrony_leapsectz` - Defines the location of the leap second file that Chrony uses to adjust for leap second corrections. Ensures accurate timekeeping during leap second events.
* `chrony_log_enable` - Enables or disables logging in Chrony, allowing administrators to track time synchronization details for analysis and debugging.
* `chrony_logdir_path` - Specifies the directory where Chrony should store log files, ensuring organized storage of synchronization data.
* `chrony_log_options` - Defines specific logging options, such as tracking measurements, statistics, and system corrections, to provide detailed insights into time synchronization.
* `chrony_ntp_clients` - Configures Chrony to allow or deny NTP clients from synchronizing with the system as an NTP server, enabling or restricting external systems from querying the local time.

### Logrotate Configuration

* `chrony_logrotate_options.archive_directory_path` - Specifies the directory where rotated log files should be stored. This helps in organizing archived logs separately from active log files.
* `chrony_logrotate_options.frequency` - Defines how often the logs should be rotated (e.g., daily, weekly, monthly). Ensures logs do not grow indefinitely and are archived periodically.
* `chrony_logrotate_options.count` - Sets the number of old log files to retain before they are deleted. Helps manage disk space while keeping a history of logs.
* `chrony_logrotate_options.missingok` - Prevents Logrotate from displaying errors if the specified log file is missing. Ensures smooth execution even if logs were not generated.
* `chrony_logrotate_options.compress` - Enables compression of rotated log files, typically using gzip, to save disk space while preserving log history.
* `chrony_logrotate_options.nocreate` - Prevents Logrotate from creating a new empty log file after rotation. Useful when the application handles log file creation itself.
* `chrony_logrotate_options.copytruncate` - Truncates the original log file after copying its contents to a rotated file. Useful for applications that keep writing to the same log file without reopening it.
* `chrony_logrotate_options.dateext` - Appends the date to rotated log filenames instead of using incremental numbers. This helps in tracking logs based on when they were rotated.

## Dependencies

None.

## Testing

This role uses Molecule for testing. To run the tests:

```bash
molecule test
```

The role is also tested using GitHub Actions, which runs:
- yamllint
- molecule tests

## Example Playbook

Using the role is fairly straightforward:
```yaml
- hosts: server
  roles:
    - role: chrony
      vars:
        chrony_role_action: "all"
        chrony_service_enabled: true
        chrony_configure_logrotate: true
        chrony_ntp_source_mode: "pool"
        chrony_ntp_servers:
          - 169.254.169.254
```

## Licenses

The
[Apache-2.0](https://github.com/grzegorzfranus/chrony/blob/main/LICENSE)
License.

If you have some other use in mind, contact me.

## Author Information

This role was created by **[Grzegorz Franus](https://github.com/grzegorzfranus)**.