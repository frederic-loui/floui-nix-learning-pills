# Nix Package operation
## Find package whose name starts with `mc` string
```
nix@buster-nix:~$ nix-env -qa 'mc.*'
mc-4.8.26
mcabber-1.1.2
mcelog-175
mcfly-0.5.6
mcomix3-unstable-2020-11-23
mcpp-2.7.2
mcrcon-0.7.1
mcrl2-201707
mcron-1.0.6
mcrypt-2.6.8
mcy-2020.08.03
```
## Install package `mc`
```
nix@buster-nix:~$ nix-env -i mc
installing 'mc-4.8.26'
...
```
## Uninstall package `mc`
```
nix@buster-nix:~$ nix-env -e mc
uninstalling 'mc-4.8.26'
building '/nix/store/91981qmlrnnqc1j6ixkcnqf9kxh0fasp-user-environment.drv'...
created 6 symlinks in user environment
```
## Upgrading package `mc`
```
nix@buster-nix:~$ nix-env -u mc
```
## Unconditionnally replace package `mc`
```
# Even if mc is already installed
nix@buster-nix:~$ nix-env -i mc
```

