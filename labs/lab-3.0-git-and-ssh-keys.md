# Lab 3.0: Git & SSH keys

### Summary

This lab was very straightforward and a very nice review of git and ssh keys. It's funny to me with the SSH keys because I have done this a few times before when setting up reverse ssh on campus so I can host my website and other utils. I will say the hardest part of this lab was the script just because the wording on it was a little funny but, once I asked a classmate I was rolling at Mach-5

### Git

* `git clone <url>` clones repo to current location
* `git commit` commits current changes to repo
  * `git commit -m <message>` will change update message in repo after push
* `git push` pushes changes that have been committed to the repo
* `git add .` adds current directory to repo
* `git pull` pulls all updates from repo
* `git checkout` checks for updates in the repo

### SSH

* `ssh-keygen -t rsa -C "<user>"` will generate a public and private rsa key pair
  * these keys will be default saved in `/home/<user>/.ssh/id_rsa`
  * THE PUBLIC KEY SAYS id\_rsa.pub NEVER SHARE PRIVATE KEY!!!!!
* For password less entry to another system
  1. copy the public key over to the `/home/<user>/.ssh/authorized_keys`
  2. `chmod 700 /home/<user>/.ssh`
  3. `chmod 600 /home/<user>/.ssh/authorized_keys`
  4. `shown -R <user>:<user> /home/<user>/.ssh`
