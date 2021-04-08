2 Choices:
* Using any Linux flavor or MacOS
* NixOS

For both choices 2 possibilities:
Single user Nix installation:  
 
As root:
```
adduser nix
mkdir /nix
chown nix /nix
```
As any standard Linux user: (e.g nix)
```
sh <(curl -L https://nixos.org/nix/install) --no-daemon
```
Multi user Nix installation:   
As root:
```
adduser nix
usermod -aG wheel nix
```
As any standard Linux user: (e.g nix)
```
sh <(curl -L https://nixos.org/nix/install) --daemon
```
note: sudo will be invoked in order to issue actions requiring root privileges.  

For simplicity's sake, I'll start my Nix journey with a `single-user` installation: 
* All Nix magic will occur into `/nix` and `/home/nix`
* It'll be easier to get rid of nix simply by `rm -rf /nix` and remove `nix` user

