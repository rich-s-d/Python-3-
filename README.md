# Python-3-

## File and Paths
```py
from pathlib import Path

data_folder = Path("source_data/text_files/")

file_to_open = data_folder / "raw_data.txt" # If you want to add on to the path, you can use the / operator directly in your code.

print(file_to_open.read_text())


if not filename.exists():
    print("Oops, file doesn't exist!")
else:
    print("Yay, the file exists!")
```
To make paths compatible in all operating systems (windows uses the opposite slash to everythin else) use:
```py
from pathlib import Path

filename = Path("source_data/text_files/raw_data.txt")
```
Here’s an example that will open a local file in your web browser with just two lines a code:
```py
from pathlib import Path
import webbrowser

filename = Path("source_data/text_files/raw_data.txt")

webbrowser.open(filename.absolute().as_uri())
```
```py
from pathlib import Path

file_name = Path(file_path).name  # myfile.png
file_stem = Path(file_path).stem  # myfile
```
