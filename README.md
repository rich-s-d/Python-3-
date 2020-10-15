# Python-3-

## Control Flow
### While Loops
```py
c = 5
while c != 0:
    print(c)
    c -= 1
```
### Break
```py
while True: #Infinite loop.
    response = input()
    if int(response) % 7 == 0:
        break
```
## Strings, Collections and Iterations
### Strings and String Literals
Be aware of escape functions. Use r (raw) if need be, ie. path = r"C:etc/etc/etc"
```py
/n #New line.
string = "This is a string with a /n new line"

string.capitalize() #One of type string's functions.
```
### List
```py
list = [3,4,"Daniel"]
list.append("rich")

list("Rich")
#returns ["r","i","c","h"]
```
### Dictionary
Dictionaries map keys to value
```py
d = {'daniel':37,'maike':29}
d['daniel'] #Returns 37
d['maike']=30 #Updates the value to 30 from 29

### Bytes
Bytes are like strings. b'string'. To change bytes to string
```py
from urllib.request import urlopen
story = urlopen('http://sixty-north.com/c/t.txt')
story_words = []
for line in story:
    line_words = line.decode('utf-8').split() #.decode('utf-8') will decode bytes to string.
    for word in line_words:
        story_words.append(word)
story.close()
story_words
```
## Pandas and Geopandas
### Functions
```py
df.apply() #Functions
```
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
