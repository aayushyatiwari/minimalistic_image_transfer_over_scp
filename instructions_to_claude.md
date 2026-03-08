# idea 
- goal is to take a picture from my pc, send it over using scp

# final product 
this is what i want 
final product should be:
i write 
```bash
./share --image_path ~/Pictures/xyz.jpg --scpIP sourav@xyxip.ip.ip --scpPassword xyz 
```
and the picture is transfered over scp in a .txt file

# plan
what we need 
- share python script using argparse library

# implementation details

## step 1 — read and encode the image
- open the image file from `--image_path`
- encode it to base64 using python's `base64` library
- base64 turns binary image data into plain text, so it can live inside a `.txt` file

## step 2 — write to a .txt file
- write the base64 string into a temp `.txt` file (e.g. `image_transfer.txt`)
- store it temporarily in `/tmp/`

## step 3 — transfer over scp
- use the `subprocess` library to call `scp` from within python
- use `sshpass` to pass the password non-interactively:
  ```bash
  sshpass -p <password> scp /tmp/image_transfer.txt <scpIP>:~/
  ```
- `sshpass` must be installed on the system: `sudo apt install sshpass`

## step 4 — cleanup
- delete the temp `.txt` file from `/tmp/` after transfer

## dependencies
- python stdlib only: `argparse`, `base64`, `subprocess`, `os`
- system tool: `sshpass`

## file structure
```
project/
  share          ← the python script (no .py extension, made executable)
```

## making the script executable
```bash
chmod +x share
```
add this shebang at the top of the script:
```python
#!/usr/bin/env python3
```

## argparse arguments
| argument | required | description |
|---|---|---|
| `--image_path` | yes | path to the image on local machine |
| `--scpIP` | yes | user@host for scp destination |
| `--scpPassword` | yes | password for scp |
