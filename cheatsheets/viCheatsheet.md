## vi commands

| Command      | Description |
| ----------- | ----------- |
| `:q`      | Quit file       |
| `:q!`   | Quit without saving changes        |
| `:w`   | Save changes to file        |
| `:wq`  <br> `:x` <br> `ZZ (shift+zz)`| Save changes and exit        |
| `:wqa`   | Save changes and exit all  tabs        |
|`:x` | Save file with encryption|
|`:80` | Jump to line 80|
|`80\|` | Jump to column 80 (`\|` is a pipe sign)|
|`i` |insert before the cursor|
|`I` |insert at the beginning of the line|
|`a` |insert (append) after the cursor|
|`A` |insert (append) at the end of the line|
|`o` |append (open) a new line below the current line|
|`O` |append (open) a new line above the current line|
|`:sp file`| Open `file` in a horizontal split |
|`:vsp file`|  Open `file` in a vertical split |
|`Ctrl+ww`|  Switch between currently opened files in splits |
|`g+t/T`|  Switch between currently opened files in tabs |
| `dd`   | Delete the current line        |
| `D`   | Delete the rest of the line on the right of the cursor        |
| `7dd`   | Delete next 7 line        |
| `:3,7d`   | Delete  line 3 to line 7        |
| `:.,7d`   | Delete current line to line 7 (`.` means current line)        |
| `:7,$d`   | Delete  line 7 to end of the file (`$` means last line)        |
| `:.,$d`   | Delete current line to end of the file      |
|`yy` <br> `Y`| Copy the current line|
| `7yy`   | Copy next 7 line        |
| `:3,7y`   | Copy  line 3 to line 7        |
| `:.,7y`   | Copy current line to line 7      |
| `:7,$y`   | Copy  line 7 to end of the file      |
| `:.,$y`   | Copy current line to end of the file      |
|`:2,7w newfile`| Copy line 2 to 7 of the current file and save it in `newfile`|
|`:2,7w! oldfile`| Copy line 2 to 7 and overwrite the existing `oldfile`|
|`p`|Paste after the current line|
|`P`|Paste after the current line|
|`r`|Replace current letter|
|`R`|Replace all letter until `ESC` is pressed|
|`gg`| Go to the start of the file|
|`G`| Go to the end of the file|
|`0`|Jump to the start of the line|
|`$`|Jump to the end of the line|
|`u`|Un do |
|`Ctrl+r`|Re do |
|`>>`| indent (move right) line one shiftwidth|
|`<<`| de-indent (move left) line one shiftwidth|
|`Ctrl+n`| Show autocomplete suggestion |
|`gi`| Go to last edited position |
|`/pattern`|Search for `pattern`|
|`*`|Search the current word under cursor|
|`n`|Go to next search result|
|`N`|Go to previous search result|
|`:%s/old/new/g`| Replace all occurrence of `old` with `new`|
|`:%s/old/new/gc`| Replace all occurrence of `old` with `new` but ask for confirmation|
|`:w !sudo tee "%"`|Save file as root after editing as non-root|



### vi command line flags
| Command      | Description |
| ----------- | ----------- |
| `vi -o file1 file2`      | Open files in horizontal split       |
| `vi -O file1 file2`      | Open files in vertical split       |
| `vi -p file1 file2`      | Open files in tabs       |
| `vi +n file`      | Open file directly on line n       |
| `vi -x file`      | Open file with encryption       |
