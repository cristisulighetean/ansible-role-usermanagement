# Ansible Role: User Management

This role provides user management on a Linux system, including creating users, assigning them to groups, and setting up their SSH keys for authentication.

## Role Variables

Available variables are listed below, along with default values (see defaults/main.yml):

```yaml
group_name: mygroup
users: []
public_key_path: "/path/to/public/key"
```

- `group_name` is the name of the group that the users will be added to.
- `users` is a list of users to be created on the system. Each user is defined as a dictionary with the keys name and password_hash. For example:

```yaml
users:
  - name: user1
    password_hash: hash1
  - name: user2
    password_hash: hash2
```

- `public_key_path` is the path to the public key file that will be added to the `authorized_keys` file of each user.

## Example Playbook

Here's an example playbook using this role:

```yaml
- hosts: servers
  roles:
    - ansible-role-usermanagement
```

To use this role with custom variables, include them either in your playbook, command line or in a separate file like so:


```yaml
- hosts: servers
  roles:
    - ansible-role-usermanagement
  vars:
    group_name: developers
    users:
      - name: dev1
        password_hash: passwordhash1
      - name: dev2
        password_hash: passwordhash2
    public_key_path: "/path/to/your/public/key"
```

## Notes

To get the password hash you could use the following:
- mkpasswd (linux)
- [mkpasswd utility](https://github.com/myENA/mkpasswd) (written in go for portability)