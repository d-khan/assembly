# Use this code to install NASM and GDB debugger

```
#!/bin/bash
sudo apt update
sudo apt install nasm
sudo apt install gdb
```

Create a file in Linux with a filename ```install.sh``` and copy the above contents in there.
For example
```
nano install.sh
```

After copying the contents, use CTRL+X to save the file.

Once the file is created, make the file executable. Use the following command.
```
chmod 711 ./install.sh
```

After the file permission has changed, use the following command to run the script.
```
./install.sh
```

