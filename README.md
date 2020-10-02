# Kali Linux LXD GUI

Clone this repository:

`git clone https://github.com/thirdbyte/kali-lxd-gui`

Change directory:

`cd kali-lxd-gui`

Run the following commands one by one: (Tested on **Ubuntu 19.10** & **Ubuntu 20.04**)

```
snap install lxd
lxd init
lxc profile create gui
cat kali-lxd-gui-profile | lxc profile edit gui
lxc launch --profile default --profile gui images:kali/current/amd64 kali
lxc exec kali -- sh -c 'echo "deb http://archive.kali.org/kali kali-rolling main contrib non-free" > /etc/apt/sources.list'
lxc exec kali -- apt-get update
lxc exec kali -- apt-get dist-upgrade -y
lxc exec kali -- apt-get install kali-linux-core kali-desktop-xfce -y
lxc exec kali -- adduser kali
lxc exec kali -- usermod -aG sudo kali
lxc exec kali -- sed -i '1 i\TERM=xterm-256color' /home/kali/.bashrc
lxc exec kali -- sh -c 'echo "export DISPLAY=:0" >> /home/kali/.bashrc'
lxc exec kali -- sh -c 'echo "cd ~" >> /home/kali/.bashrc'
lxc exec kali -- sh -c "echo 'Set disable_coredump false' > /etc/sudo.conf"
lxc exec kali -- apt install xfce4-terminal -y
lxc exec kali -- apt remove qterminal -y
lxc exec kali -- apt-get autoremove -y
lxc exec kali -- apt-get clean
lxc exec kali -- sudo -u kali xfce4-panel
```
![](/kali-lxd-gui.png)

That's it!
--
Original documentation : [https://www.kali.org/docs/containers/kalilinux-lxc-images/#gui-kali-lxd-container-on-ubuntu-host](https://www.kali.org/docs/containers/kalilinux-lxc-images/#gui-kali-lxd-container-on-ubuntu-host)
Thanks to Simos Xenitellis for GUI profile: [https://blog.simos.info/wp-content/uploads/2018/06/lxdguiprofile.txt](https://blog.simos.info/wp-content/uploads/2018/06/lxdguiprofile.txt)
