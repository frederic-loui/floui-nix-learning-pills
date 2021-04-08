# Nix upgrade on Linux
## single-user mode
```
nix-channel --update 
nix-env -iA nixpkgs.nix
```
## multi-user mode (valid also for NixOs)
```
sudo nix-channel --update
sudo nix-env -iA nixpkgs.nix
```
