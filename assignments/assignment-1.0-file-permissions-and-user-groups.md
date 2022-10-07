# Assignment 1.0: File Permissions & User Groups

### Commands

[Cheat Sheet](https://www.google.com/search?q=linux+file+permissions+cheat+sheet\&tbm=isch\&ved=2ahUKEwjF8ursiqDzAhV9gXIEHdR\_AnkQ2-cCegQIABAA\&oq=linux+file+permi\&gs\_lcp=CgNpbWcQARgAMgUIABCABDIECAAQQzIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBggAEAgQHjIGCAAQCBAeMgYIABAIEB4yBggAEAgQHlD9HFjEIGCUJ2gAcAB4AIABXIgB4wKSAQE1mAEAoAEBqgELZ3dzLXdpei1pbWfAAQE\&sclient=img\&ei=zzVSYYXPM\_2CytMP1P-JyAc\&bih=1286\&biw=1278\&rlz=1C1GCEA\_enUS969US969#imgrc=1IiTJQl4N2J4tM)

#### Steps to create user and add to group

1. `useradd example_user` = will add user of selected name
2. `passwd example_user` = makes it so you can create password for user
3. `groupadd example_group` = will create the new group
4. `usermod -aG example_group example_user` = this will add user to a selected group
5. `su - example_user` = will become that user
6. `chgrp example_group /example_directory` = will apply the example\_group to the example\_directory
7. `chmod` = will allow you to change permission for file/directory
   * `chmod g+rwx /example_directory or file` = will allow the group permission to read, write, and execute
   * `chomd g-rwx /example_directory or file` = will get rid of the ability to read, write, and execute for the group permissions
   * `g` = is for group
   * `o` = is for other
   * `chomd g-rwx *` = all files in current directory will be effected
   * `chomd -v num example_file` = will change permissions using binary to decimal
     * num is decimal number like '600' = for this the owner gets r and w (r+w = 6) and 0 means no permissions for the other sections
     * read = 100 (binary) = 4
     * write = 010 (binary) = 2
     * execute = 001 (binary) = 1
8. `id` = shows what groups and uid for logged in user
9. `echo text >> /example_directory/example.txt` = will append text to example.txt
10. `echo text > /example_directory/example.txt` = will over write text to example.txt and or create file example.txt with text in it

Side notes

1. `chown example_user example_file` = Will change the owner of the file to specified owner

#### List commands

1. `ls` = shows directories in current directory
   * `ls -l /example` = will show all the files in directory \* drwxr-xr-- owner group file/directory name \* drwxrw-r-- owner group file/directory name \* drwx-wxrw- owner group file/directory name
   * `ls -ld /example` = listing directory instead of at the file level \* example: drwx------ owner group directory name
2. `drwxrwxrwx` = who can read write and exicute
   * first 4 are the owner
   * next 3 are the group
   * last 3 are what others can do
   * drwx------ owner group file/directory name
     * only the owner would be able to see read write and exicute this file/directory
