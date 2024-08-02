# Useful Linux commands

## Resource starvation
On a Linux machine, you can identify processes that are using excessive amount of CPU or memory by running gnome-system-monitor and sorting by % CPU or by Memory.

Alternatively, use the top command:

```sh
top -o %CPU # sort by CPU usage
top -o %MEM # sort by memory usage
```


## check your dir size
```sh
df -h .
```
## Useful shell commands

```sh
du -h <dir>      # print the estimated file space usage of the directory
df | grep <user> # check the available file space of your mounted directories
```
