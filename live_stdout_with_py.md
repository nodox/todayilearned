# How to stream or poll stdout from a python script

I created an automated script at work to run `psql` commands via python for better control flow.
Unlike bash, python does not stream the output to STDOUT. You have to wait for the program to finish
to capture everything from STDOUT. Here is what feels like a decent way to output to STDOUT in realtime.

```python
#!/usr/bin/python
import subprocess, sys, shlex
## command to run - tcp only ##
cmd = "netstat -p tcp -f inet"

p = subprocess.Popen(shlex.split(cmd), shell=True, stderr=subprocess.PIPE, encoding="utf-8")
 
## Display output live, immediately 
while True:
    out = p.stderr.read(1)r
    if out == '' and p.poll() is not None:
        break
    if out != '':
        sys.stdout.write(out)
        sys.stdout.flush()
```
