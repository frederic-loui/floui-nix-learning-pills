# Nix profile
Nix `profile` combined with `user-env` symlinks will give users using Nix the possibility to enjoy multiple distinct profiles. 
In order to understand the profiles key feature let's assume the following example:
* we are running a [`RARE router`](https://wiki.geant.org/display/RARE) on a `WEDGE100Bf32X` hardware.
* The user running this RARE control plane and dataplane is the Linux user `rare`
* On `WEDGE100BF32X` is powered by a Programmable Ethernet Asic called TOFINO
* TOFINO ensure is the magic silicon that based on a user written program using the language P4 switch ingress packet at 6.4 Tbps and soon 12.8 Tbps
* However in order to reach such speed TOFINO, there is a trade off. TOFINO has a limited amount of resources burnt into the silicon
  (A formula one can reach 233 mph but obviously you cannot put a lot of luggage in a MacLaren)
* However, RARE software is versatile and flexible enough to so that you can implement on the `WEDGE100BF32X`multiple profile. Each profile corresponding to a specific usage of the `WEDGE100BF32X`
* Practically, this profile is obtained by tailoring and recompiling the P4 same program

You have guessed it. Nix is providing an elegant and absolutely reproducible compilation of each profile and isolated environment.
In this precise case, `rare` user can have `bier`,`pppoe`,`rawip`, `mpls` profile for example in dedicated Nix profile. Each of one of them having a user-env encompassing the respective P4 compilation.
