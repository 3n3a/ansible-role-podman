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

## options

| option | default | description |
| --- | --- | --- |
| `podman_package_state` | present | state that packages (podman, python3-cryptography) will have when running this role |
| `podman_systemd_scope` | system | can only be system right now. user mode is untested and buggy in podman. |
| `podman_add_quadlet` | false | add quadlet directory |
| `podman_quadlet_path` | /etc/containers/systemd | directory where quadlets will be saved to and expected at. depends on systemd_scope |
| `podman_add_auto_update` | false | add auto-update trigger for podman |
| `podman_auto_update_on_calendar` | daily | auto-update daily at 00:00. [documentation of options](https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html) |
| `podman_add_prometheus` | false | setup podman prometheus exporter |
| `podman_prometheus_port` | 9882 | port on which prometheus metrics are available |
| `podman_prometheus_image` | quay.io/navidys/prometheus-podman-exporter:latest | image which is setup with add_prometheus |