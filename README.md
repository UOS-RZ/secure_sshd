# Example Ansible playbook including secure\_sshd

This branch contains a fully functional example playbook using the role `secure_sshd`.

The files explained:

- [`ansible.cfg`](ansible.cfg): General ansible configuration and role locations
- [`deploy.yml`](deploy.yml): Ansible Playbook including the `secure_sshd` role
- [`hosts.yml`](hosts.yml): Inventory file specifying the hosts to run the playbook on
- [`requirements.yml`](requirements.yml): Requirements file specifying dependencies for `ansible-galaxy`

## Quick Start

1. Make sure you can ssh into the hosts you want to configure without password (e.g. using an SSH key).

2. Edit the [`hosts.yml`](hosts.yml) to configure the host(s) you want to run this on:
    ```yaml
      hosts:
        host01.example.com:
        host02.example.com:
    ```

3. Install the `secure_sshd` role:
    ```
    ❯ ansible-galaxy install -r requirements.yml
    ```

4. Deploy SSH server configuration to all hosts:
    ```
    ❯ ansible-playbook deploy.yml
    ```

## Custon Configuration

There are several ways to set variables in Ansible.
For this example, we set the option to prevent `root` login via SSH globally as part of the role inclusion.

Edit [`deploy.yml`](deploy.yml) and set:

```yml
  roles:
    - role: secure_sshd
      sshd_root_login: 'no'
```

## Role Version

You can specify the exact version of the `secure_sshd` role you want in `requirements.yml`.
To update to a newer version, edit the file and set the version you want:

```yaml
- src: https://github.com/UOS-RZ/secure_sshd.git
  scm: git
  version: 1.1.0
```

The force an update by running `ansible-galaxy`:
```
❯ ansible-galaxy install --force -r requirements.yml
```
