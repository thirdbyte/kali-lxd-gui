# Kali Linux LXD GUI

Clone this repository:

`git clone https://github.com/thirdbyte/kali-lxd-gui`

Change directory:

`cd kali-lxd-gui`

Run the following commands one by one: (Tested on **Ubuntu 19.10**)

```
sudo snap install lxd
lxd init

lxc profile create gui
cat kali-lxd-gui-profile | lxc profile edit gui
lxc launch --profile default --profile gui images:kali/current/amd64 kali

lxc exec kali -- sh -c 'echo "deb http://archive.kali.org/kali kali-rolling main contrib non-free" > /etc/apt/sources.list'
lxc exec kali -- apt update
lxc exec kali -- apt install kali-linux-light kali-desktop-xfce

lxc exec kali -- adduser kali
lxc exec kali -- usermod -aG sudo kali
lxc exec kali -- sed -i '1 i\TERM=xterm-256color' /home/kali/.bashrc
lxc exec kali -- sh -c 'echo "export DISPLAY=:0" >> /home/kali/.bashrc'
lxc exec kali -- sh -c "echo 'Set disable_coredump false' > /etc/sudo.conf"

lxc exec kali -- apt install xfce4-terminal nano net-tools build-essential curl wget git
lxc exec kali -- apt remove qterminal

lxc exec kali -- sudo -u kali xfce4-panel
```

That's it!
