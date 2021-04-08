# nix generation
Nix has a `generation` concept that basically identify the state of a Nix distribution installation
## List Nix generation
```
nix@buster-nix:~$ nix-env --list-generations
   1   2021-04-08 09:24:42   
   2   2021-04-08 16:02:28   
   3   2021-04-08 16:03:53   
   4   2021-04-08 16:10:04   (current)
```
In the example above, the command list 4 generations, that corresponded to the following states:
1- install `mc`
2- remove `mc`
3- build `mc`
4- install `mc`


```
nix@buster-nix:~$ date
Thu 08 Apr 2021 05:12:42 PM CEST
```

```
nix@buster-nix:~$ git
-bash: git: command not found
```

```
nix@buster-nix:~$ nix-env -i git
warning: there are multiple derivations named 'git-2.31.0'; using the first one
installing 'git-2.31.0'
...

created 350 symlinks in user environment
nix@buster-nix:~$ date
Thu 08 Apr 2021 05:20:10 PM CEST
nix@buster-nix:~$ nix-env --list-generations
   1   2021-04-08 09:24:42   
   2   2021-04-08 16:02:28   
   3   2021-04-08 16:03:53   
   4   2021-04-08 16:10:04   
   5   2021-04-08 17:20:03   (current)
```   
