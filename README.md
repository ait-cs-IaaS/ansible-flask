# Ansible Role: flask

Install a flask app and run as a service

## Requirements

- Ansible 2.10+
- Debian-based linux-distribution

## Dependencies

[grog.user](https://github.com/GROG/ansible-role-user)

## Role Variables

### General

```yaml
flask_app_name: "flask-app" # Name of the app

flask_user: "www-data" # Owner of the app
flask_usergroup: "{{ flask_user }}"
flask_user_password: "password"
```

### Setup
```yaml
flask_paths: # App directories
  base: "/var/www/{{ flask_app_name }}"
  log: "/var/log/{{ flask_app_name }}"
```

### Git & Access
```yaml
GIT_ACCESS_TOKEN: "{{ lookup('env', 'GIT_ACCESS_TOKEN') }}" # If not set as ENV, it is prompted for

flask_git: # Repo to clone the app from
  user: "git-user"
  repo: "flask-app-repo-name"
  token: "{{ GIT_ACCESS_TOKEN }}"
  branch: "master"
  force: yes
  always_reinstall: yes # If 'yes' the directory is cleared before cloning
```

### Systemd service
```yaml
flask_service_files: # Template file definitions
  service:
    template: "flask.service.j2"
    destination: "/etc/systemd/system/{{ flask_app_name }}.service"
  socket:
    template: "flask.socket.j2"
    destination: "/etc/systemd/system/{{ flask_app_name }}.socket"
```


## Configuration example

## Licence

GPL-3.0

## Author information

Lenhard Reuter