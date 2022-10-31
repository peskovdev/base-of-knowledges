Automaticly open locked second storage
1. Create random key
```
dd if=/dev/random bs=32 count=1 of=/etc/key_file_hdd
```
2. Add this keyfile as key for luks-hdd:
```
cryptsetup luksAddKey /dev/sdx1 /etc/key_file_hdd
```
3. Add to `/etc/crypttab` following line:
```
# UUID of disk: /dev/sdXn
cryptmedia     UUID=f19e0bb5-f7d1-4834-abb6-a44f179d302f    /etc/key_file_hdd       luks,discard
```
4. Add to `/etc/fstab` following line:
```
# UUID of disk: /dev/mapper/cryptmedia
UUID=feac531b-fb20-4eb3-88bb-ea23709379e7	/media     	ext4     	defaults        1 2
```

That's all. crypttab will unlock your disk as `/dev/mapper/cryptmedia`, fstab mount `cryptmedia` to your directory
