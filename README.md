# share — image transfer over SCP

a command line tool that transfers an image from your pc to a remote machine over scp, inspired by how MIME encodes binary data in SMTP.

PS: i built this while studying for my computer networks exam       

## how it works
1. encodes the image to base64 (plain text)
2. writes it to a temp `.txt` file
3. transfers the `.txt` file to the remote machine via scp
4. decodes it back into an image on the remote machine
5. cleans up the temp file

## dependencies
- python 3
- `sshpass` — install with `sudo apt install sshpass`

## usage
```bash
./share --image_path ~/Pictures/xyz.jpg --scpIP user@192.168.x.x --scpPassword yourpassword
```

## arguments
| argument | description |
|---|---|
| `--image_path` | path to the image on your local machine |
| `--scpIP` | `user@host` of the recipient machine |
| `--scpPassword` | scp password |


## output
the decoded image is saved on the recipient's machine at `~/decoded_image`

## setup
```bash
chmod +x share
```
