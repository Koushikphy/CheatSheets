#### List directories only: 
```bash
ls -d <location>*/
```  

#### Copy files with progress and speed shown:
```
rsync -avh --progress --ignore-times
```

#### set date and time directly from terminal:
```
sudo date -s "$(wget -qSO- --max-redirect=0 google.in 2>&1 | grep Date: | cut -d' ' -f5-8)Z"
```

#### vi search and replace
```
:%s/foo/bar/g
```

#### vi open multiple files simultaneously
```
vi FILE1 FILE2 ... -O/-o
```

#### bash print two file side by side 
```
pr FILE1 FILE2 -m 
```

#### bash follow a file every N seconds
```
watch -n N FILE
```