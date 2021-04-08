# Nix channel on Linux
After having installed Nix package manager you'd expect to install some packages from one or sevreral repositories similar to Debian or Redhat package manager.
Nix comes with a default set of packages called **Nix packages collection**. Once you installed Nix, this install a default channel.
## List channel
This list the channel that is currently active. Below you see the default channel installed.
```
nix@buster-nix:~$ nix-channel --list
nixpkgs https://nixos.org/channels/nixpkgs-unstable
nix@buster-nix:~$ 
```
note: Nix is not dependent on any package collection. You can create your own channel and use it instead.

## Add channel
```
$ nix-channel --add https://nixos.org/channels/nixpkgs-unstable
$ nix-channel --update
```
## Delete channel
```
$ nix-channel --remove https://nixos.org/channels/nixpkgs-unstable
$ nix-channel --update
```
## Rollback channel
Nix supports a concept called `generation`. If after an `update` you are not satisfied you can rollbac your system to previous generation.
```
$ nix-channel --rollback `generation`
$ nix-channel --update
```
## update channel
```
nix-channel --update 
```
note to self: As a start, we are considering a mono repository model, that i presume translate into using one channel. How to handle software installation when having several channels ? (multiple calls of `nix-channel --add <my_additional_channel>`) 
