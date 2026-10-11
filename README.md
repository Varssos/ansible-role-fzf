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

## Manual setup (without Ansible)

```bash
sudo apt install fzf bat
find /usr/share/doc -name key-bindings.bash -print -quit
```

Add a `source` line for the path returned by `find` to your `~/.bashrc`,
then add the following configuration once:

```bash
export FZF_DEFAULT_OPTS="--style full"
export FZF_COMPLETION_TRIGGER='**'
export FZF_CTRL_T_OPTS="
  --walker-skip .git,node_modules,target
  --preview 'batcat -n --color=always {}'
  --bind 'focus:transform-header:file --brief {}'"
source /usr/share/doc/fzf/examples/completion.bash
```

Open a new Bash session. These options require a sufficiently recent fzf;
older distribution packages may not support `--style` or `--walker-skip`.

## License

MIT

## Author

Varssos
