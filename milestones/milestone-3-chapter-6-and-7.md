# Milestone 3 (Chapter 6 and 7)

## Chapter 6 Cross Compiling Temporary Tools

### 6.2.1. Installation of M4

Prepare M4 for compilation:

```
./configure --prefix=/usr   \
            --host=$LFS_TGT \
            --build=$(build-aux/config.guess)
```

Compile the package:

```
make
```

Install the package:

```
make DESTDIR=$LFS install
```

### 6.3.1. Installation of Ncurses



First, ensure that **gawk** is found first during configuration:

```
sed -i s/mawk// configure
```

Then, run the following commands to build the “tic” program on the build host:

```
mkdir build
pushd build
  ../configure
  make -C include
  make -C progs tic
popd
```

Prepare Ncurses for compilation:

```
./configure --prefix=/usr                \
            --host=$LFS_TGT              \
            --build=$(./config.guess)    \
            --mandir=/usr/share/man      \
            --with-manpage-format=normal \
            --with-shared                \
            --without-normal             \
            --with-cxx-shared            \
            --without-debug              \
            --without-ada                \
            --disable-stripping          \
            --enable-widec
```

Compile the package:

```
make
```

Install the package:

```
make DESTDIR=$LFS TIC_PATH=$(pwd)/build/progs/tic install
echo "INPUT(-lncursesw)" > $LFS/usr/lib/libncurses.so
```
