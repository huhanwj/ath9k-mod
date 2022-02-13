# ath9k-mod
disable CSMA/CA in ath9k
Bulit on the backport project with kernel version of 5.3-rc4.

## Main Modification
* Disable CSMA in ath9k.
* Disable backoff in ath9k.
* Configure the chip as HCF Poll Gated via register configuration.

##  Installation
### System requirement
Ubuntu (with kernel version <= 5.3)

### Dependencies
```Shell
sudo apt update
sudo apt-get install build-essential bison bc flex libncurses5-dev libncursesw5-dev libssl-dev libelf-dev
```

### Install the backport kernel
```Shell
make defconfig-ath9k
make -j<n>
sudo make install -j<n>
```

Note here that the `-j<n>` is used for accelerating the compiling process. The number n is select according to the number of threads that your CPU have, you may check it from `cat /proc/cpuinfo`.

Finally, reboot the system to make it work.
