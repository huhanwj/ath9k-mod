# ath9k-mod
disable CSMA/CA in ath9k
Bulit on the backport project with kernel version of 4.4.2.

## Main Modification
* Disable CSMA in ath9k.
* Disable backoff in ath9k.
* Configure the chip as HCF Poll Gated via register configuration.

##  Installation
### System requirement
Ubuntu 14.04(with kernel version <= 4.4.2)

### Dependencies
```Shell
sudo apt update
sudo apt-get install build-essential bison bc flex libncurses5-dev libncursesw5-dev libssl-dev libelf-dev
```

### Install the backport kernel
```Shell
make defconfig-ath9k-debug
make -j<n>
sudo make install -j<n>
```

Note here that the `-j<n>` is used for accelerating the compiling process. The number n is select according to the number of threads that your CPU have, you may check it from `cat /proc/cpuinfo`.

Finally, reboot the system to make it work.

## Usage
### Disabling Carrier Sense

Execute this:

```bash
test@ubuntu:~$ sudo su
root@ubuntu:~$ mount -t debugfs none /sys/kernel/debug
root@ubuntu:~$ cd /sys/kernel/debug/ieee80211/phy*/ath9k/registers/
root@ubuntu:~$ echo 1 > force_channel_idle
root@ubuntu:~$ echo 1 > ignore_virt_cs
```

Writing 1 to `force_channel_idle` disables physical carrier sense (channel is busy). Writing 1 to `ignore_virt_cs` disables virtual carrier sense (RTS/CTS). Random backoff parameters can also be changed.
