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

## Example

```
# ./imgclone -s 60088320 -s 60082176 -n "USB SanDisk 3.2Gen1" my_image.img
Considering 3 disk(s):
   /dev/sdb        USB SanDisk 3.2Gen1                       57.3 GiB
   /dev/sdc        USB SanDisk 3.2Gen1                       57.3 GiB
   /dev/sde        USB SanDisk 3.2Gen1                       57.3 GiB
Proceed with 4 dd processes? Type 'YES': YES
Started dd on /dev/sdb
Started dd on /dev/sdc
Started dd on /dev/sde
30720+0 records in
30720+0 records out
32212254720 bytes (32 GB, 30 GiB) copied, 1642 s, 19,6 MB/s
Finished dd on /dev/sdc after 1642 secs
30720+0 records in
30720+0 records out
32212254720 bytes (32 GB, 30 GiB) copied, 2075,03 s, 15,5 MB/s
Finished dd on /dev/sdb after 2075 secs
30720+0 records in
30720+0 records out
32212254720 bytes (32 GB, 30 GiB) copied, 2269,23 s, 14,2 MB/s
Finished dd on /dev/sde after 2269 secs
Finished after 2269 secs
```


## License
GNU GPL-3.
