The aliases can be found here.
ref:- https://github.com/BhattJayD/my-useful-comands-and-scripts

### Initial scan
```
nmap $IP -Pn -sVC -oN initial -A -vvv
```

### Full port scan
```
nmap -p --min-rate 10000 -vvv -oN full
```

### Initial scan for only open port 
```bash
initial $IP -p $(grep /tcp full |awk '{print $1}' | cut -d'/' -f1 |paste -sd,)
```

##### **Command Explanation**

```bash
$(grep /tcp full | awk '{print $1}' | cut -d'/' -f1 | paste -sd,)
```

1. **`grep /tcp full`**
    - Searches for lines containing `/tcp` in the file named `full`.
    - This assumes `full` contains network scan results (e.g., from our full `nmap` port scan).
2. **`awk '{print $1}'`**
    - Extracts the first column from the filtered results.
3. **`cut -d'/' -f1`**
    - Splits each line at the `/` character and takes the first part.
    - This removes `/tcp` and leaves only the port number.
4. **`paste -sd,`**
    - Joins all extracted port numbers into a single comma-separated string.

**Example Input (content of `full`)**
```
22/tcp  open  ssh
80/tcp  open  http
443/tcp open  https
```
**Command Output**
```
22,80,443
```

