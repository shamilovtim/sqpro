# sqpro - Quake 1 Linux Server

Current version: 3.93

Credits: ID Software, J.P. Grossman, Baker, r00k, Spike, slotzero, en0ch, omicron, probably others

sqpro is used as a Linux server popularly used to run Quake 1 Netquake. It is used primarily for CRMOD (CTF, Deathmatch) but can run anything.
A prebuilt 32 bit binary has been provided as part of this package but compilation instructions are also provided.
sqpro is currently incompatible to compile to 64 bit and must be run as a 32bit binary.

## Compilation
sqpro compiles as "unixded" and you are free to rename it back to sqpro.

Make sure you have all needed prerequisites:

Add 32 bit support:
```shell
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 g++-multilib build-essential
```

Compile sqpro:
```shell
make unixded
```

While sqpro compiles from `unixded` there are several other compilations in the Makefile including full blown GLQuake. Be sure not to compile any of the other stuff and stick to `unixded`.

## Configure your server and enable anticheat
In your autoexec.cfg setup the server and be sure to use `sv_cullentities 2` for autocheat. Example of a useful config:
```
sv_aim 2
sys_ticrate 0.04
sv_cullentities 2
rcon_password 9999
name "serveradmin"

// initial map
map dm3
```


## Other tips for your server
Edit `/etc/crontab` and add the following to restart your server at 5am nightly, adjusting for `cd` to the path of your sqpro binary.
```shell
0  5    * * * root reboot
@reboot root cd /home/debian/quakeserver/ && ./sqpro -mem 256 -port 26000 -dedicated 16 -game crmod -condebug "$(date +\%Y\%m\%d)" -zone 1024 +hostname "My Deathmatch Server"
```