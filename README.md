# tips
So I don't ever need to google this shit again

# Vim

`:terminal`

`Ctrl+w N` Enter normal mode from terminal

`i` exit normal mode (enter insert mode) to terminal

`:w terminal.log` write terminal buffer to file from normal mode

`Ctrl+w [hjkl]` switch to pane left/down/up/right

`Ctrl+w [HJKL]` move pane left/down/up/right

`Ctrl+s` fucks up vim. `Ctrl+q` to unfuck

# Linux

`timeout 5 sleep 10` Auto stop a program after some time

`unbuffer buffered_writes.bin | tee out.log` Unbuffer buffered stdout - see Python below

# Bash

```bash
lines=`cat $1`
for line in $lines
do
  echo $line;
done
```

`${variable/match/replace}` parameter expansion replace (not regex - you can do shit like `file_*`)

`${variable//match/replace}` parameter expansion global replace

# Python

`python3 -u writes_to_stdout.py` Write to stdout unbuffered

`python3 -u writes_to_stdout.py | tee out.log` This is why writing unbuffered matters

`python3 -u handles_ctrl_c.py | tee -i out.log` Have tee ignore SIGINT and let Python handle it

```python3
import requests
from requests.packages.urllib3.exceptions import InsecureRequestWarning
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)
requests.get(url, verify=False)
```
I know I don't have the CA cert, shut up

```python3
import argparse, sys

def parse_args():
  parser = argparse.ArgumentParser(description='text')
  parser.add_argument('-s', '--short', type=str, help='text')
  parser.add_argument('-b', '--boolean', action='store_true', help='text')
  if len(sys.argv) == 1:
    parser.print_help()
    sys.exit(1)
  args = parser.parse_args()
  return args

args = parse_args()
print(args.short)
print(args.boolean)
```

# SQL

`SELECT col FROM table LIMIT [OFFSET], [QUANTITY]` iterate over offset with quantity 1 to get row-by-row

`SUBSTRING("test", [OFFSET], [QUANTITY])=` iterate over offset with quantity 1 to get char-by-char

# MySQL

`@@version`

`user()`

`database()`

`SELECT table_name FROM information_schema.tables` MySQL get table names. Can also filter default tables `WHERE table_schema != "mysql"`

`SELECT column_name FROM information_schema.columns WHERE table_name = "table"` MySQL get column names of table
