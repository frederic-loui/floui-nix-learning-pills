# Nix upgrade
## single-user mode
```
nix-channel --update; nix-env -iA nixpkgs.nix
```
## multi-user mode
```
sudo nix-channel --update; nix-env -iA nixpkgs.nix
```
