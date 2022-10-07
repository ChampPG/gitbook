# Tar

## Documentation

{% embed url="https://man7.org/linux/man-pages/man1/tar.1.html" %}

## Options

```
-c : Creates Archive 
-x : Extract the archive 
-f : creates archive with given filename 
-t : displays or lists files in archived file 
-u : archives and adds to an existing archive file 
-v : Displays Verbose Information 
-A : Concatenates the archive files 
-z : zip, tells tar command that creates tar file using gzip 
-j : filter archive tar file using tbzip 
-W : Verify a archive file 
-r : update or add file or directory in already existed .tar file 
```

## Usage

### **Creating an uncompressed tar Archive using option -cvf**

This command creates a tar file called file.tar which is the Archive of all .c files in current directory.

```bash
tar -cvf <file-name>.tar *.c
```

**Output:**

```
os2.c
os3.c
os4.c
```

### **Extracting files from Archive using option -xvf**

This command extracts files from Archives.

```bash
tar -xvf <file-name>.tar
```

**Output:**

```bash
os2.c
os3.c
os4.c
```

### **gzip compression on the tar Archive, using option -z**&#x20;

This command creates a tar file called file.tar.gz which is the Archive of .c files.

```bash
tar -cvzf <file-name>.tar.gz *.c
```

### **Extracting a gzip tar Archive \*.tar.gz using option -xvzf**&#x20;

This command extracts files from tar archived file.tar.gz files.

```bash
tar -xvzf <file-name>.tar.gz
```

### **Creating compressed tar archive file in Linux using option -j**&#x20;

This command compresses and creates archive file less than the size of the gzip. Both compress and decompress takes more time then gzip.

```bash
tar -cvfj <file-name>.tar.tbz example.cpp
```

Output

```bash
$ tar -cvfj <file-name>.tar.tbz example.cpp
example.cpp
$ tar -tvf <file-name>.tar.tbz
-rwxrwxrwx root/root        94 2017-09-17 02:47 example.cpp
```

### **Untar single tar file or specified directory in Linux**&#x20;

This command will Untar a file in current directory or in a specified directory using -C option.

```bash
$ tar -xvfj file.tar 
or 
$ tar -xvfj file.tar -C <path-of-file-in-dir> 
```

### **Untar multiple .tar, .tar.gz, .tar.tbz file in Linux**

This command will extract or untar multiple files from the tar, tar.gz and tar.bz2 archive file. For example the above command will extract “fileA” “fileB” from the archive files.

```bash
$ tar -xvf <file-name>.tar "fileA" "fileB" 
or 
$ tar -zxvf <file-name>.tar.gz "fileA" "fileB"
or 
$ tar -jxvf <file-name>.tar.tbz "fileA" "fileB"
```

### **Check size of existing tar, tar.gz, tar.tbz file in Linux**

The above command will display the size of archive file in Kilobytes(KB).

```bash
$ tar -czf <file-name>.tar | wc -c
or 
$ tar -czf <file-name1>.tar.gz | wc -c
or 
$ tar -czf <file-name2>.tar.tbz | wc -c
```

### **Update existing tar file in Linux**

```bash
tar -rvf <file-name>.tar *.c
```

**Output:**

```
os1.c
```

### **List the contents and specify the tarfile using option -tf**&#x20;

This command will list the entire list of archived file. We can also list for specific content in a tarfile

```bash
tar -tf <file-name>.tar
```

**Output:**

```
example.cpp
```

### **Applying pipe to through ‘grep command’ to find what we are looking for**

This command will list only for the mentioned text or image in grep from archived file.

```bash
$ tar -tvf <file-name>.tar | grep "text to find" 
or
$ tar -tvf <file-name>.tar | grep "filename.file extension"
```

### **We can pass a file name as an argument to search a tarfile**

This command views the archived files along with their details.

```bash
tar -tvf <file-name>.tar filename
```

### **Viewing the Archive using option -tvf**&#x20;

```bash
tar -tvf <file-name>.tar
```

**Output:**

```
-rwxrwxrwx root/root       191 2017-09-17 02:20 os2.c
-rwxrwxrwx root/root       218 2017-09-17 02:20 os3.c
-rwxrwxrwx root/root       493 2017-09-17 02:20 os4.c
```

### **Wildcards**&#x20;

Alternatively referred to as a ‘wild character’ or ‘wildcard character’, a wildcard is a symbol used to replace or represent one or more characters. Wildcards are typically either an asterisk (\*), which represents one or more characters or question mark (?),which represents a single character.

### **To search for an image in .png format**

This will extract only files with the extension .png from the archive file.tar. The –wildcards option tells tar to interpret wildcards in the name of the files to be extracted; the filename (_.png) is enclosed in single-quotes to protect the wildcard (_) from being expanded incorrectly by the shell.

```bash
tar -tvf <file-name>.tar --wildcards '*.png' 
```
