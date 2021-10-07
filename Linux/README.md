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


#### bash print two file side by side 
```
pr FILE1 FILE2 -m 
```


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

#### use function with `xargs`
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
ls -l /proc/<proc_id>/exe
```

#### rsync only copy file with certain extension
copy files only with `.sh` [extension](https://stackoverflow.com/questions/11111562/rsync-copy-over-only-certain-types-of-files-using-include-option/11111793)
```
rsync -zarvm --include="*/" --include="*.sh" --exclude="*" "$from" "$to"
```


#### `rsync` only transfer certain files  
search the list of files with `fd` (or `find`) and send it using `rsync`
```bash
fd <serach_pattern> | rsync -arvm --files-from=- $src $dst
```