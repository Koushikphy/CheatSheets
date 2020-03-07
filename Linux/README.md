#### List directories only: 
```bash
ls -ld -- */
```  

#### Copy files with progress and speed shown:
```
rsync -avh --progress --ignore-times
```

#### set date and time directly from terminal:
```
sudo date -s "$(wget -qSO- --max-redirect=0 google.in 2>&1 | grep Date: | cut -d' ' -f5-8)Z"
```