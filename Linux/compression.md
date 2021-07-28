## Compress files
Using `gzip`: 

```bash
gzip -kv -6 <filename>
#or
gzip -kvr -6 <directory>
```
`-k` : is to keep the original file after genereting the compressed one, by defualt it removes the original file.   
`-v` is for `verbose`.   
`-6` is the (default) compression level, available number are from 1 to 9, 1 being the fastest and 9 meaning the best/slowest compression.   
For directory `-r` flag is used for recursive compression.  

Decompress the same with 
```bash
gzip -d file.gz
```

Similar to `gzip` another compression utility `bzip2`. It has similar flags and usage like `gzip`  
For parallel gzip use https://zlib.net/pigz/  



---
Using `xz`:  
`xz`(`lzma` compression) is better alternative to `gzip` use it with 
```bash
xz -k -6 -T 3 --verbose <file>
```
`xz` supports parallel processing, use it wtih `-T 3` with 3 being number of processor.  

For best possible compression use https://github.com/ckolivas/lrzip  

[A Quick Benchmark: Gzip vs. Bzip2 vs. LZMA](https://tukaani.org/lzma/benchmarks.html)  

Which one to use?  
* If you want to quickly compress the file and on a limited resource use `gzip`. 
* If you want the best compression/ smallest file size and have enough RAM and processor available use `xz`

---
## Compress folder/directory
Usually linux folder compression is done by first archiving the folder in a file, usually by `tar` then using a compression utility on it. Gnu `tar` can handle this whole process on its own.
```bash
tar -zcvf archive.tar.gz sample-folder
```
`-z` : Use `gzip` to compress  
`-c` : Create archilve  
`-v` : Verbose  
`-f` : Archive file name  
`-j` : Use `bzip2` utility  
`-J` : Use `xz` utility  
`-I` : Specify compression utility, `-I 'gzip -6'` is same as `-z`  
To decompress the file into the folder again replace the create (`-f`) with extract (`-x`) flag use
```bash
tar -zxvf archive.tar.gz
```  
