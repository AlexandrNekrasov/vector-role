# vector-role

Ansible role for installing and configuring [Vector](https://vector.dev/) — a lightweight, ultra-fast tool for building observability pipelines.

## Requirements

- Ubuntu 20.04 / 22.04
- Ansible 2.10+

## Role Variables

### defaults/main.yml

| Variable | Description | Default |
|----------|-------------|---------|
| `vector_version` | Version of Vector to install | `0.21.1` |
| `vector_install_dir` | Installation directory | `/opt/vector` |
| `vector_data_dir` | Data directory for Vector | `/var/lib/vector` |
| `vector_config_dir` | Config directory | `/etc/vector` |
| `vector_user` | User to own data dir | `ubuntu` |
| `vector_group` | Group to own data dir | `ubuntu` |

### vars/main.yml

| Variable | Description |
|----------|-------------|
| `vector_archive_url` | Full URL to Vector archive (computed from `vector_version`) |
| `vector_archive_dir` | Name of extracted directory |
| `vector_archive_path` | Path to downloaded archive on target host |

## Dependencies

None.

## Example Playbook

    - hosts: vector
      roles:
        - role: vector-role
          vars:
            vector_version: "0.21.1"
            vector_install_dir: "/opt/vector"

## Tasks

1. Install `ca-certificates`, `tar`, `gzip`
2. Download Vector archive
3. Unarchive to `/opt/`
4. Rename directory to `{{ vector_install_dir }}`
5. Create config and data directories
6. Deploy `vector.toml` config from template
7. Ensure Vector is running

## Handlers

- **Restart vector service** — restarts Vector via `pkill` + `nohup`

## License

MIT

## Author Information

AlexandrNekrasov
