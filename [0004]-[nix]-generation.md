# Nix generation
Nix has a `generation` concept that basically identify the state of a Nix distribution installation on a per Nix `profile` basis
## List Nix generation
```
nix@buster-nix:~$ nix-env --list-generations
   1   2021-04-08 09:24:42   
   2   2021-04-08 16:02:28   
   3   2021-04-08 16:03:53   
   4   2021-04-08 16:10:04   (current)
```
In the example above, the command list 4 generations, that corresponded to the following states:
1. install `mc`
2. remove `mc`
3. build `mc`
4. install `mc` (pointer indicating the current generation in use)
## Generation in Nix store
```
nix@buster-nix:~$ ls -l /nix/var/nix/profiles/per-user/nix/
total 20
lrwxrwxrwx 1 nix nix 15 Apr  8 09:24 channels -> channels-1-link
lrwxrwxrwx 1 nix nix 60 Apr  8 09:24 channels-1-link -> /nix/store/w2nlim1f8522cwhvb39gv21acy7pcafl-user-environment
lrwxrwxrwx 1 nix nix 14 Apr  8 16:10 profile -> profile-4-link
lrwxrwxrwx 1 nix nix 60 Apr  8 09:24 profile-1-link -> /nix/store/cvqjv2c8dzww5gmwddlbs5d12lnxysqw-user-environment
lrwxrwxrwx 1 nix nix 60 Apr  8 16:02 profile-2-link -> /nix/store/in7d8w4mb3vh1ry9ry57bpz508z9jlzi-user-environment
lrwxrwxrwx 1 nix nix 60 Apr  8 16:03 profile-3-link -> /nix/store/gwxxjbh8v9p0m6gn3zi8m9bmlggraxc4-user-environment
lrwxrwxrwx 1 nix nix 60 Apr  8 16:10 **profile-4-link -> /nix/store/in7d8w4mb3vh1ry9ry57bpz508z9jlzi-user-environment**
```
Check 4th generation symlink `<4th-generation-symlink>/bin`
```
nix@buster-nix:~$ ls -l /nix/store/in7d8w4mb3vh1ry9ry57bpz508z9jlzi-user-environment/bin
total 64
lrwxrwxrwx 1 nix nix 60 Jan  1  1970 mc -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mc
lrwxrwxrwx 1 nix nix 64 Jan  1  1970 mcdiff -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mcdiff
lrwxrwxrwx 1 nix nix 64 Jan  1  1970 mcedit -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mcedit
lrwxrwxrwx 1 nix nix 64 Jan  1  1970 mcview -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mcview
lrwxrwxrwx 1 nix nix 62 Jan  1  1970 nix -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix
lrwxrwxrwx 1 nix nix 68 Jan  1  1970 nix-build -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-build
lrwxrwxrwx 1 nix nix 70 Jan  1  1970 nix-channel -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-channel
lrwxrwxrwx 1 nix nix 78 Jan  1  1970 nix-collect-garbage -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-collect-garbage
lrwxrwxrwx 1 nix nix 75 Jan  1  1970 nix-copy-closure -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-copy-closure
lrwxrwxrwx 1 nix nix 69 Jan  1  1970 nix-daemon -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-daemon
lrwxrwxrwx 1 nix nix 66 Jan  1  1970 nix-env -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-env
lrwxrwxrwx 1 nix nix 67 Jan  1  1970 nix-hash -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-hash
lrwxrwxrwx 1 nix nix 74 Jan  1  1970 nix-instantiate -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-instantiate
lrwxrwxrwx 1 nix nix 75 Jan  1  1970 nix-prefetch-url -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-prefetch-url
lrwxrwxrwx 1 nix nix 68 Jan  1  1970 nix-shell -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-shell
lrwxrwxrwx 1 nix nix 68 Jan  1  1970 nix-store -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-store
```

## Software installation impact on generation
`git` is not installed
```
nix@buster-nix:~$ git
-bash: git: command not found
```
thus, let's install it as an example.
```
nix@buster-nix:~$ nix-env -i git
warning: there are multiple derivations named 'git-2.31.0'; using the first one
installing 'git-2.31.0'
...
created 350 symlinks in user environment
```
Check the time.
```
nix@buster-nix:~$ date
Thu 08 Apr 2021 05:20:10 PM CEST
```
List generation again
```
nix@buster-nix:~$ nix-env --list-generations
   1   2021-04-08 09:24:42   
   2   2021-04-08 16:02:28   
   3   2021-04-08 16:03:53   
   4   2021-04-08 16:10:04   
   5   2021-04-08 17:20:03   (current)
```
As you can see a new generation has been created.
In the Nix store you can also see the symlink designating the 5th generation related to the software distribution after `git` installation
```
nix@buster-nix:~$ ls -l /nix/var/nix/profiles/per-user/nix/
total 24
lrwxrwxrwx 1 nix nix 15 Apr  8 09:24 channels -> channels-1-link
lrwxrwxrwx 1 nix nix 60 Apr  8 09:24 channels-1-link -> /nix/store/w2nlim1f8522cwhvb39gv21acy7pcafl-user-environment
lrwxrwxrwx 1 nix nix 14 Apr  8 17:20 profile -> profile-5-link
lrwxrwxrwx 1 nix nix 60 Apr  8 09:24 profile-1-link -> /nix/store/cvqjv2c8dzww5gmwddlbs5d12lnxysqw-user-environment
lrwxrwxrwx 1 nix nix 60 Apr  8 16:02 profile-2-link -> /nix/store/in7d8w4mb3vh1ry9ry57bpz508z9jlzi-user-environment
lrwxrwxrwx 1 nix nix 60 Apr  8 16:03 profile-3-link -> /nix/store/gwxxjbh8v9p0m6gn3zi8m9bmlggraxc4-user-environment
lrwxrwxrwx 1 nix nix 60 Apr  8 16:10 profile-4-link -> /nix/store/in7d8w4mb3vh1ry9ry57bpz508z9jlzi-user-environment
lrwxrwxrwx 1 nix nix 60 Apr  8 17:20 profile-5-link -> /nix/store/9b678lmcypij6qd491l28sdsxch5rmlw-user-environment
```
Check 5th generation symlink `<5th-generation-symlink>/bin`
```
ls -l /nix/store/9b678lmcypij6qd491l28sdsxch5rmlw-user-environment/bin/
total 96
lrwxrwxrwx 1 nix nix 62 Jan  1  1970 git -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git
lrwxrwxrwx 1 nix nix 79 Jan  1  1970 git-credential-netrc -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git-credential-netrc
lrwxrwxrwx 1 nix nix 72 Jan  1  1970 git-cvsserver -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git-cvsserver
lrwxrwxrwx 1 nix nix 75 Jan  1  1970 git-http-backend -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git-http-backend
lrwxrwxrwx 1 nix nix 75 Jan  1  1970 git-receive-pack -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git-receive-pack
lrwxrwxrwx 1 nix nix 68 Jan  1  1970 git-shell -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git-shell
lrwxrwxrwx 1 nix nix 77 Jan  1  1970 git-upload-archive -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git-upload-archive
lrwxrwxrwx 1 nix nix 74 Jan  1  1970 git-upload-pack -> /nix/store/xianfgmb08p08yn0hfyg0w3szhgmz1mc-git-2.31.0/bin/git-upload-pack
lrwxrwxrwx 1 nix nix 60 Jan  1  1970 mc -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mc
lrwxrwxrwx 1 nix nix 64 Jan  1  1970 mcdiff -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mcdiff
lrwxrwxrwx 1 nix nix 64 Jan  1  1970 mcedit -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mcedit
lrwxrwxrwx 1 nix nix 64 Jan  1  1970 mcview -> /nix/store/gry78g7nfr84fyzna4lw3d7awhmnnn5w-mc-4.8.26/bin/mcview
lrwxrwxrwx 1 nix nix 62 Jan  1  1970 nix -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix
lrwxrwxrwx 1 nix nix 68 Jan  1  1970 nix-build -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-build
lrwxrwxrwx 1 nix nix 70 Jan  1  1970 nix-channel -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-channel
lrwxrwxrwx 1 nix nix 78 Jan  1  1970 nix-collect-garbage -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-collect-garbage
lrwxrwxrwx 1 nix nix 75 Jan  1  1970 nix-copy-closure -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-copy-closure
lrwxrwxrwx 1 nix nix 69 Jan  1  1970 nix-daemon -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-daemon
lrwxrwxrwx 1 nix nix 66 Jan  1  1970 nix-env -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-env
lrwxrwxrwx 1 nix nix 67 Jan  1  1970 nix-hash -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-hash
lrwxrwxrwx 1 nix nix 74 Jan  1  1970 nix-instantiate -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-instantiate
lrwxrwxrwx 1 nix nix 75 Jan  1  1970 nix-prefetch-url -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-prefetch-url
lrwxrwxrwx 1 nix nix 68 Jan  1  1970 nix-shell -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-shell
lrwxrwxrwx 1 nix nix 68 Jan  1  1970 nix-store -> /nix/store/iwfs2bfcy7lqwhri94p2i6jc87ih55zk-nix-2.3.10/bin/nix-store
```
Can you spot that `git` is in this 5th generation folder ? 
