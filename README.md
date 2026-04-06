# hashicorp-aap-playbooks

These playbooks are intended for quick tests/demos in Ansible Automation Platform (AAP) against **RHEL-family** hosts and **Amazon Linux 2023**.

## Playbooks

### `install_docker.yml`
Installs Docker Engine (Docker CE), enables/starts the service, and installs Docker Compose v2 plugin.

**Optional vars**
- `docker_users`: list of users to add to `docker` group (e.g. `["ec2-user"]`)

Run:
```bash
ansible-playbook -i inventory playbooks/install_docker.yml -e '{"docker_users":["ec2-user"]}'
```

### `install_nginx.yml`
Installs and starts NGINX and drops a simple demo `index.html`. Attempts to open firewall ports 80/443 via firewalld (best effort).

Run:
```bash
ansible-playbook -i inventory playbooks/install_nginx.yml
```

### `install_websphere.yml` (skeleton)
This is a **skeleton** for IBM WebSphere Application Server installation because IBM media is not redistributable.

You must stage/provide:
- Installation Manager installer directory on the managed host (`im_installer_path`)
- WAS repository directory on the managed host (`was_repository_path`)
- Silent install response file (`was_response_file_path`)

Run example:
```bash
ansible-playbook -i inventory playbooks/install_websphere.yml \
  -e im_installer_path=/tmp/IM \
  -e was_repository_path=/tmp/WAS_REPO \
  -e was_response_file_path=/tmp/was_response.xml
```

### `install_open_liberty.yml`
Downloads and installs Open Liberty from IBM public distribution, creates a server, and installs a systemd unit.

**Common vars**
- `liberty_version` (default: `24.0.0.12`)
- `liberty_http_port` (default: `9080`)
- `liberty_server_name` (default: `defaultServer`)

Run:
```bash
ansible-playbook -i inventory playbooks/install_open_liberty.yml
```