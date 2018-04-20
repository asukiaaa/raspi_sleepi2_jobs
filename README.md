# raspi sleepi2 jobs
Example jobs to run on a Raspberry Pi with using slee-Pi2.

# Components
- Raspberry Pi Zero WH
- [slee-Pi2](https://mechatrax.com/products/slee-pi/)

# Tested Environment

```
$ cat /etc/os-release
PRETTY_NAME="Raspbian GNU/Linux 9 (stretch)"
NAME="Raspbian GNU/Linux"
VERSION_ID="9"
VERSION="9 (stretch)"
ID=raspbian
ID_LIKE=debian
HOME_URL="http://www.raspbian.org/"
SUPPORT_URL="http://www.raspbian.org/RaspbianForums"
BUG_REPORT_URL="http://www.raspbian.org/RaspbianBugs"
```

```
$ uname -a
Linux raspberrypi 4.14.34+ #1110 Mon Apr 16 14:51:42 BST 2018 armv6l GNU/Linux
```

# Setup

Install tools for slee-Pi2

```
sudo bash -c 'echo "deb http://mechatrax.github.io/raspbian/ stretch main contrib non-free" > /etc/apt/sources.list.d/mechatrax.list'
wget http://mechatrax.github.io/raspbian/pool/main/m/mechatrax-archive-keyring/mechatrax-archive-keyring_2016.12.19.1_all.deb
sudo dpkg -i mechatrax-archive-keyring_2016.12.19.1_all.deb
sudo apt update
sudo apt install -y sleepi2-firmware sleepi2-utils sleepi2-monitor
```

# Usage

## alarm

Add alarm command to `/etc/rc.local` before `exit 0` like this.

```
{
  sleep 20

  # Add jobs what you want

  [path for this dir]/alarm --set-eariest "02:00JST, 14:00JST"
  if [ "`sleepi2alarm --get`" = "" ]
  then
    sleepi2alarm --set "+10min"
  fi
  poweroff
} || {
  # on error
  sleepi2alarm --set "+10min"
  poweroff
} &
```

Raspberry Pi will wake up at 01:00JST, 13:00JST or 14:00JST.

# References
- [mechatrax/slee-pi2](https://github.com/mechatrax/slee-pi2)
- [mechatrax/sleepi2-utils](https://github.com/mechatrax/sleepi2-utils)
- [sleepi2alarm](https://github.com/mechatrax/sleepi2-utils/blob/master/sleepi2alarm)
