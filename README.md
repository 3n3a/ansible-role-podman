# ansible role podman

setup podman on a centos based server (fedora, rhel).

## example playbook

```yaml
- name: Setup Podman
  hosts: all
  become: true
  vars_files:
    - vars/main.yml
  roles:
  - podman
```

in vars/main.yml

```yaml
# adds quadlet support
podman_add_quadlet: true

# adds auto update trigger for tagged pods, default daily 00:00
podman_add_auto_update: true

# creates quadlet that exports podman prometheus metrics, default port 9882
podman_add_prometheus: true
```

### install directly from here

add the following to your `requirements.yml`

```yaml
---
roles:
  - name: 3n3a.podman
    src: git+ssh://git@github.com:22/3n3a/ansible-role-podman.git
    version: master
    scm: git
```