# Nix installation options
## 2 operating systems:
* Using any Linux flavor or MacOS
* NixOS

## 2 possibilities when using Linux/MacOS (NixOS is multi-user):
* **Single-user Nix installation:**  
 
As `root`:
```
adduser nix
mkdir /nix
chown nix /nix
```
As `nix` standard Linux user:
```
sh <(curl -L https://nixos.org/nix/install) --no-daemon
```
* **Multi-user Nix installation:**   
As `root`:
```
adduser nix
usermod -aG wheel nix
```
As `nix` standard Linux user:
```
sh <(curl -L https://nixos.org/nix/install) --daemon
```
note: `sudo` will be invoked in order to issue actions requiring `root` privileges.  
## My personal choice:** (motivated by learning's sake)   
For simplicity's sake, I'll **start my Nix journey** with a `single-user` installation: 
* All Nix magic will occur into `/nix` and `/home/nix`
* It'll be easier to get rid of nix simply by `rm -rf /nix` and remove `nix` user

