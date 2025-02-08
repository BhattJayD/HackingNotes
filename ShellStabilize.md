```python3
python3 -c "import pty;pty.spawn('/bin/bash')"
```

``ctrl + z``

```bash
stty raw -echo;fg
```

```bash
stty rows 47 columns 211
```

```bash
export TERM=xterm-256color
```

```bash
alias l="ls -lath --color"
```

oneliner

```bash
stty rows 47 columns 211;export TERM=xterm-256color;alias l="ls -lath --color"
```
