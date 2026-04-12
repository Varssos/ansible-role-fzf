# fzf

Ansible role to install [fzf](https://github.com/junegunn/fzf) fuzzy finder and configure key bindings on Debian/Ubuntu systems.

## Requirements

- Debian or Ubuntu host
- `become: true` privileges (sudo)

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `fzf_package_name` | `fzf` | Package name to install via apt |
| `fzf_shells` | `[~/.bashrc]` | List of shell rc files to add fzf key bindings to |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: fzf
```

Override variables if needed (e.g. add zsh support):

```yaml
- hosts: all
  become: true
  roles:
    - role: fzf
      vars:
        fzf_shells:
          - "/home/myuser/.bashrc"
          - "/home/myuser/.zshrc"
```

## License

MIT

## Author

Varssos
