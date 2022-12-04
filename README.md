# imgclone
imgclone is a tool intended to clone one block device image on many USB sticks
in parallel. The idea is that you safely identify the devices by their name
(e.g., brand) and exact size (in blocks) so that during many "dd" operations,
you do not accidently overwrite a disk dear to you. It identifies all devices
(e.g., USB sticks) that match the criteria and then parallelizes the writing
operation on them (simply invoking parallel dd processes).

``` 
usage: imgclone [-h] [-p count] [-n name] [-s blocks] [-r regex] [-v]
                img_filename

Clone a disk image onto multiple USB sticks at the same time.

positional arguments:
  img_filename          Image filename to clone

options:
  -h, --help            show this help message and exit
  -p count, --parallel count
                        How many dd processes to run concurrently. Defaults to
                        4.
  -n name, --disk-name name
                        Disk name to require. Must match that of hdparm -i.
                        Defaults to USB SanDisk 3.2Gen1.
  -s blocks, --disk-size blocks
                        Disk size to enforce, in blocks. Must match that in
                        /proc/partitions. Defaults to 60082176.
  -r regex, --disk-regex regex
                        Disk regex to consider. Defaults to sd[a-z].
  -v, --verbose         Increases verbosity. Can be specified multiple times
                        to increase.
```

## License
GNU GPL-3.
