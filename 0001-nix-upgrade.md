# Nix upgrade on Linux
## single-user mode
```
nix-channel --update 
nix-env -iA nixpkgs.nix
```
## multi-user mode 
```
sudo nix-channel --update
sudo nix-env -iA nixpkgs.nix
```
## NixOs
```
sudo nix-channel --update
sudo nixos-rebuild switch
```

