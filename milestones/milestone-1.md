# Milestone 1

### Mothership

#### Specs

OS: [Xubuntu 20.04.5 amd 64](http://mirror.us.leaseweb.net/ubuntu-cdimage/xubuntu/releases/20.04/release/xubuntu-20.04.5-desktop-amd64.iso)\
Memory: 8GB\
vCPU: 4threads\
Storage: 1x40GB & 1x30GB SCSI disk\
&#x20;   \- Second disk is called `mothership-0.vmdk`\
&#x20;Boot: BIOS

![](<../.gitbook/assets/image (3) (2).png>)

### Startup Commands

```
sudo apt install ssh
mkdir ./lfs
sudo mkdir /mnt/lfs
```

### Version Check

```
sudo apt install build-essential
sudo apt dist-upgrade
```

```
cat > version-check.sh << "EOF"
#!/bin/bash
# Simple script to list version numbers of critical development tools
export LC_ALL=C
bash --version | head -n1 | cut -d" " -f2-4
MYSH=$(readlink -f /bin/sh)
echo "/bin/sh -> $MYSH"
echo $MYSH | grep -q bash || echo "ERROR: /bin/sh does not point to bash"
unset MYSH
echo -n "Binutils: "; ld --version | head -n1 | cut -d" " -f3-
bison --version | head -n1
if [ -h /usr/bin/yacc ]; then
echo "/usr/bin/yacc -> `readlink -f /usr/bin/yacc`";
elif [ -x /usr/bin/yacc ]; then
echo yacc is `/usr/bin/yacc --version | head -n1`
else
echo "yacc not found"
fi
echo -n "Coreutils: "; chown --version | head -n1 | cut -d")" -f2
diff --version | head -n1
find --version | head -n1
gawk --version | head -n1
if [ -h /usr/bin/awk ]; then
echo "/usr/bin/awk -> `readlink -f /usr/bin/awk`";
elif [ -x /usr/bin/awk ]; then
echo awk is `/usr/bin/awk --version | head -n1`
else
echo "awk not found"
fi
EOF
```

Make executable and run

```
sudo chmod +x ./version-check.sh
bash version-check.sh
```

Output from the first `./version-check.sh` pass

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

**FIX:**&#x20;

```
sudo apt install bison binutils gawk
sudo ln -sf bash /bin/sh
```

Output after installing all dependencies

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### Partitioning Scheme

/dev/sdb needs to be partitioned

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>lsblk output</p></figcaption></figure>

#### Setup Partitions

```
sudo -i
cfdisk /dev/sdb
```

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>cfdisk output</p></figcaption></figure>

Now select `Write` and type `yes`

`lsblk` after cfdisk

<figure><img src="../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

```
mkfs.ext2 /dev/sdb2 -L LFSBOOT
mkfs.ext4 /dev/sdb3 -L LFSROOT
mkfs.ext4 /dev/sdb4 -L LFSHOME
mkswap /dev/sdb5
```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Command Outputs</p></figcaption></figure>

```
lsblk -f /dev/sdb
```

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption><p>/dev/sdb partitioned</p></figcaption></figure>

### Setting $LFS (2.6)

As normal user

```
exit
echo "export LFS=/mnt/lfs" >> ~/.bashrc
source ~/.bashrc
echo $LFS
```

As root user

```
sudo -i
echo "export LFS=/mnt/lfs" >> ~/.bashrc
source ~/.bashrc
echo $LFS
```

### Mounting LFS manually (2.7)

<pre><code>sudo -i
mkdir -pv $LFS
mount -c -t ext4 /dev/sdb3 $LFS
mkdir -v $LFS/home
mount -c -t ext4 /dev/sdb4 $LFS/home
<strong>swapon /dev/sdb5</strong></code></pre>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Mount on Boot

```
nano /etc/fstab
```

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

```
reboot
lsblk
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
