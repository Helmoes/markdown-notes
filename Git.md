File states:
  - Modified: you have changed the file but have not committed it to your database yet.
  - Staged: you have marked a modified file in its current version to go into your next commit snapshot.
  - Committed: the data is safely stored in your local database.

`git init` creates .git subdirectory with all repo files.

![[Difference-Between-Commit-and-Push.png|800]]
![[Difference-Between-Commit-and-Push-.png|800]]

# General commands
```bash
git help <command>
git <command> --help (full ) -h (short in terminal)

git branch -m main <BRANCH>
git fetch origin
git branch -u origin/<BRANCH> <BRANCH>
git remote set-head origin -a

git branch -m main master
git fetch origin
git branch -u origin/master master
git remote set-head origin -a

git config --list -l
git config user.name
git config <section.keyname>
git config --global init.defaultBranch main

ssh-keygen 
    -E <sha256/MD5>
# Show fingerprint of specified public key file. For RSA and DSA keys ssh-keygen tries to find the matching public key file and prints its fingerprint. If combined with -v, a visual ASCII art representation of the key is supplied with the fingerprint.
    -l
    -f <filename> # Specifies the filename of the key file.
```

```bash
git remote -v # show remote url after name
```

## Git limitations
[source](https://code.visualstudio.com/docs/remote/wsl#_git-limitations)
If you clone a Git repository using SSH and your SSH key has a passphrase, VS Code's pull and sync features may hang when running remotely. Either use an SSH key without a passphrase, clone using HTTPS, or run `git push` from the command line to work around the issue.

# Windows key
```bash
$ ssh-keygen -l -f id_rsa.pub
3072 SHA256:x+cKH1xYPHGcXjpZIuytElwOaKRu3sg1jtKyB3kxK78 Willem@LAPTOP-Willem (RSA)

$ where ssh-keygen
C:\Program Files\Git\usr\bin\ssh-keygen.exe
C:\Windows\System32\OpenSSH\ssh-keygen.exe
```

# WSL key
https://docs.github.com/en/authentication/connecting-to-github-with-ssh

```bash
$ ssh-keygen -t rsa -b 4096 -C "helmoes@git.com"

The key fingerprint is:
SHA256:fZBciabR219jUlWta7FpSIdFAqGlcWC0nKU6dA6Oy+4 helmoes@git.com

git config --global user.name "WillemWSL"
git config --global user.email helmoes@git.com

eval "$(ssh-agent -s)" # don't use

ssh -T git@github.com

ssh -i 
```

# SSH
-   ssh is the SSH client component that runs on the user's local system
-   sshd is the SSH server component that must be running on the system being managed remotely
-   ssh-keygen generates, manages and converts authentication keys for SSH
-   ssh-agent stores private keys used for public key authentication
-   ssh-add adds private keys to the list allowed by the server
-   ssh-keyscan aids in collecting the public SSH host keys from hosts
-   sftp is the service that provides the Secure File Transfer Protocol, and runs over SSH
-   scp is a file copy utility that runs on SSH

