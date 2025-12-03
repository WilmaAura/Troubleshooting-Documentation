# Linux Troubleshooting

## How to make windows partition auto mount on boot without asking for password

### Check the partition

```bash
sudo blkid
```

Find your windows NTFS partition, for example:

```bash
/dev/sda3: UUID="1234-ABCD" TYPE="ntfs" PARTLABEL="Basic data partition"
```

### Make mount point folder

```bash
sudo mkdir -p /mnt/windows
```

### Add to /etc/fstab

```bash
sudo nano /etc/fstab
```

Add command like down below

```bash
UUID=1234-ABCD   /mnt/windows   ntfs-3g   defaults,noatime,uid=1000,gid=1000,umask=022 0 0
```

- uid = 1000, gid=1000 -> To get access without sudo
- umask =022 ->
- ntfs-3g -> A stable NTFS driver
- defaults -> systemd's default options

### Testing fstab without reboot

```bash
sudo mount -a
```

if there is no error -> success.
