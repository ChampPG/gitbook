# Milestone 2

### Chapter 3 Packages and Patches using wget-list-systemd

```
sudo -i
mkdir -v $LFS/sources
chmod -v a+wt $LFS/sources
exit
cd $LFS/sources
wget https://www.linuxfromscratch.org/lfs/view/stable-systemd/wget-list-systemd
wget --input-file=wget-list-systemd --continue --directory-prefix=$LFS/sources
du -h
wget https://www.linuxfromscratch.org/lfs/view/stable-systemd/md5sums
pushd $LFS/sources
  md5sum -c md5sums
popd
```

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Shows expat-2.4.8 Not installed</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Shows zlib not installed (This is due to the creators removing 1.12.2 due to a vulnerability)</p></figcaption></figure>

#### Manual Download

[https://zlib.net/zlib-1.2.13.tar.gz](https://zlib.net/zlib-1.2.13.tar.gz) As of October 13, 2022 zlib version 1.2.12 has a vulnerability so I updated to 1.2.13.

[https://sourceforge.net/projects/expat/files/expat/2.4.9/expat-2.4.9.tar.xz/download](https://sourceforge.net/projects/expat/files/expat/2.4.9/expat-2.4.9.tar.xz/download) (Previous version was labeled as critically vulnerable)

[https://www.python.org/ftp/python/3.10.8/Python-3.10.8.tar.xz](https://www.python.org/ftp/python/3.10.8/Python-3.10.8.tar.xz) (This is to fix the python vulnerability)

[https://www.python.org/ftp/python/doc/3.10.8/python-3.10.8-docs-html.tar.bz2](https://www.python.org/ftp/python/doc/3.10.8/python-3.10.8-docs-html.tar.bz2) (This is to fix the python-docs vulnerability)

#### Clean Run

To get a clean run I had to modify the md5sum file.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>How to get the format for the md5sum file</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>How the md5sum file looks</p></figcaption></figure>

Clean run:

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Showing a clean md5sum -c md5sum run</p></figcaption></figure>

### Chapter 4 - Directory Structure for LFS File System (4.2)

```
sudo -i
mkdir -pv $LFS/{etc,var} $LFS/usr/{bin,lib,sbin}

for i in bin lib sbin; do
  ln -sv usr/$i $LFS/$i
done

case $(uname -m) in
  x86_64) mkdir -pv $LFS/lib64 ;;
esac
mkdir -pv $LFS/tools
```

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>File System ls -l</p></figcaption></figure>
