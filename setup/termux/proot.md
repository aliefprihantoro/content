## install
> tutorial disini menggunakan config [ini](https://github.com/aliefprihantoro/dotconf)
```sh
pkg install mesa-zink virglrenderer-mesa-zink vulkan-loader-android virglrenderer-android
pkg install termux-x11-nightly
pkg install proot-distro
pkg install pulseaudio
pd install debian
pd login debian
```
## open debian and install some packages
```sh
ln -s /data/data/com.termux/files/home/.myconf/ $HOME
ln -s $HOME/.myconf/home/.* $HOME
mkdir .config
ln -s $HOME/.myconf/.config/* $HOME/.config/

```
> location path proot distro `/data/data/com.termux/files/usr/var/lib/proot-distro/installed-rootfs/debian`

## use zsh and setup zshrc
> update file `/etc/pam.d/chsh`, change be `auth       sufficient   pam_shells.so`
```sh
apt-get install zsh
cat >~/.zshrc <<EOF
export dr=/data/data/com.termux/files/home
export dc=\$dr/.myconf
sta() {
  rm -r .vnc/:*
  rm -r .vnc/loc*
  rm -r /tmp/.*
  vncserver -geometry 1640x720
}
staf() {
  local OPTION_USER=\$(echo "i3\nopenbox --startup \$HOME/.config/openbox/autostart\nawesome" | fzf)
  if [ ! -z \$OPTION_USER ]; then
    rm -r .vnc/:*
    rm -r .vnc/loc*
    rm -r /tmp/.*
    echo \$OPTION_USER >\$HOME/.vnc/xstartup
    vncserver -geometry 1640x720
  fi
}
alias sto='
vncserver -kill :1
'
stoo() {
  vncserver -kill :\$1
}
source \$dc/home/.zshrc
export PATH=\$PATH:\$HOME/.myconf/bin/
EOF
chmod +x ~/.zshrc
```
## setup window manager
> install 
```sh
ln -s $HOME/.myconf/home/.* $HOME
ln -s $HOME/.myconf/.config/* $HOME/.config/
```
## app

> di awal mungkin akan terjadi lag, karena belum ada cache. dan juga force close termux, agar config ter-reload. jika masih lag, atur resolusi x11 dan jangan biarkan termux dibatasi oleh penghemat baterai. Biasanya ada di pengaturan hp kalian (tergantung merk).
for install app kilck [here](../linux/apps/README.md)

### use nvim (termux installed) in proot

```sh
mkdir /libexec
ln -s /data/data/com.termux/files/usr/libexec/nvim /libexec/
ln -s /data/data/com.termux/files/usr/lib/lua* /lib/

```

## add/update custom bin
> this for i3wm and update wallpaper
```sh
cd /bin
ln -s ~/.myconf/bin/* ./
```

## fix timezone
```sh
dpkg-reconfigure tzdata
```
