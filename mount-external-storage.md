# How to Mount an SSD to a Custom Directory in Your Home Folder

This guide explains how to mount an SSD (or any drive) to a custom directory inside your `$HOME` instead of the default `/media/` path. This is useful for organizing your storage exactly how you want it.

---

## 1️Find Your SSD Device

Run:

```bash
lsblk
```

Look for your device name. Example:

```
sda           8:0    0 931.5G  0 disk
└─sda1        8:1    0 931.5G  0 part /media/desertblume/Extreme SSD
```

---

## 2️Get the UUID

Run:

```bash
sudo blkid
```

Find the UUID for your partition. Example output:

```
/dev/sda1: LABEL="Extreme SSD" UUID="545B-1942" BLOCK_SIZE="512" TYPE="exfat" PARTLABEL="Extreme SSD" PARTUUID="9985ec56-25d7-4d66-b73b-6bd5fc2316f5"
```

---

## 3️Create a Custom Mount Point

Pick a folder under your home directory. Example:

```bash
mkdir -p /home/desertblume/exssd
```

This is where the SSD will be mounted.

---

## 4️Edit `/etc/fstab`

Open `/etc/fstab` with root permissions:

```bash
sudo nano /etc/fstab
```

Add this line at the end (replace UUID if needed):

```
UUID=545B-1942   /home/desertblume/exssd   exfat   defaults   0   2
```

**Explanation:**

* `UUID=...` → uniquely identifies your SSD.
* `/home/desertblume/exssd` → custom mount point.
* `exfat` → filesystem type.
* `defaults` → use default mount options.
* `0 2` → skip dump, run `fsck` after root (not really needed for exFAT but harmless).

---

## 5️Test It

Mount everything:

```bash
sudo mount -a
```

If there are no errors, your SSD is now mounted to `/home/desertblume/exssd`.

It will mount automatically at every boot.

---

##  Notes

* Always back up `/etc/fstab` before editing.
* If you want permission support, use `ext4` instead of `exfat` (but exFAT is great for cross-platform drives).
* You can unmount safely with:

  ```bash
  sudo umount /home/desertblume/exssd
  ```

Done! Now you have full control over where your SSD lives in your file system.

Happy mounting.
