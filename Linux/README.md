#### Copy files with progress and speed shown:
```
rsync -zmavh --progress --stats
```

#### Print m to n lines of a file:
```
sed -n 'm,np' file
```

#### set date and time directly from terminal:
```
sudo date -s "$(wget -qSO- --max-redirect=0 google.in 2>&1 | grep Date: | cut -d' ' -f5-8)Z"
```

#### vi open multiple files simultaneously
```
vi FILE1 FILE2 ... -O/-o
```

#### bash print two file side by side 
```
pr FILE1 FILE2 -m 
```
<!-- 
#### bash follow a file every N seconds
```
watch -n N FILE
``` -->

#### tree with file size
```
tree -h -d 1 --du /path/to/dir
```
#### Modify file without opening it
```
sed -i "s/string/replace/g" file
```
#### Check diskIO of processes
```
sudo iotop
```

#### Pass output to a argument
```
moveRun() {
  cwd=$(pwd)
  cd $1
  pwd
  cd $cwd
}

export -f moveRun
ls -d */ | xargs -n1 bash -c 'moveRun "$@"' _
```

#### tail with timestamp
```
tail -f outputfile | xargs -IL date +"%I:%M:%S %p"
```



#### Quickly benchmark file I/O speed
```
dd if=/dev/zero of=/tmp/output conv=fdatasync bs=384k count=1k; rm -f /tmp/output
```
#### Check location of some running command
```
ls -l /proc/<proc_id>/fd
```

#### File compressions
Compress  
```
gzip -kv <filename>
#or
gzip -kvr <directory>
```

Decompress
```
gzip -d file.gz
```
A better option is to use `xz`, usually avialable by defualt in linux distros, it provide better compression than `gzip` and supports mulitple threads. For quick usage, use
```
xz -k  --fast -T <processor> --verbose <file>
```
For parallel gzip use https://zlib.net/pigz/  
For best possible compression use https://github.com/ckolivas/lrzip


#### Run command with `find`
```
find *** -exec bash -c '<command> "$0"' {} \;
```