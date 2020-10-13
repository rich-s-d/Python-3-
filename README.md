# Python-3-

## File and Paths
```py
if not filename.exists():
    print("Oops, file doesn't exist!")
else:
    print("Yay, the file exists!")
```
To make paths compatible in all operating systems, ie., /\, use:
```py
from pathlib import Path

filename = Path("source_data/text_files/raw_data.txt")
```
