# Ansible role 'ansible-role-sshd'

An Ansible role for setting up SSH connectivity.

Given that we use Ansible, SSH is assumed to be installed and running already.

The role offers the option of disabling SSH, but keep in mind that any future
interaction with the host through Ansible requires an alternative way of connecting
to be possible and actively used.

Consider that the default settings here disables root login through password, so a
ssh-key should be set up (not included in this role) before this role is run.

Config is slightly more restrictive than the regular defaults for most distros.
For example, no password authentication is allowed by default.

Kerberos authentication configuration has not been tested yet, but is in the pipeline.

## Requirements
This role has been verified to work with:
- CentOS 7
- RHEL 8
- Ubuntu 19.04
- Fedora 30

Other distributions and other versions might very well work (such as CentOS 8,
RHEL 7, Fedora 28, etc.), but no guarantees.

## Role Variables
| Variable		| Default		| Comments (type) |
| :---			| :---			| :---		  |
| `ssh_enabled` | `yes` | If set to `no`, the SSH daemon will be disabled (though not stopped unless the system is restarted). |
| `ssh_state` | `restarted` | Fed to module as `service.started` for the SSH daemon and takes the modules possibilities. |
| `ssh_daemon` | `sshd` | The name of the SSH daemon as recognized by the init system. |
| :---			| :---			| :---		  |

The following variables are available for SSHD configuration. They are only commented unless everything about it is said in the man page for sshd_config.
| `ssh_port` | `22` | The role does not actually support changing the port in respect of firewalls and SELinux, because changing port is considered bad practice. |
| `ssh_addressfamily` | `any` | |
| `ssh_listenaddresses` | ["`0.0.0.0`","::"] | List of addresses for `ListenAddress` |
| `ssh_logingracetime` | `2m` ||
| `ssh_permitrootlogin` | `prohibit_password` ||
| `ssh_maxauthtries` | `2` | |
| `ssh_authorizedkeysfile` | `.ssh/authorized_keys` | |
| `ssh_passwordauthentication` | `no` | |
| `ssh_x11forwarding` | `yes` | |

## Dependencies

## Example Playbook
```Yaml
- hosts: foo
  roles:
    - role: ansible-role-sshd
```

## Testing


## License

BSD

## Contributors

Issues, feature requests, ideas, suggestions, etc. are appreciated and can be posted in the Issues section. Pull requests are also very welcome. Please create a topic branch for your proposed changes, it's the easiest way to merge back into the project.

- [Oscar Petersson](https://github.com/oscpe262/) (Maintainer)
