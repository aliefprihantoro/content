## neovim
> [!IMPORTANT]
> see [here](../../nvim.md) for how to install and setup neovim
## vscodium
### install
```sh
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg |
  gpg --dearmor |
  dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg
echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' |
  tee /etc/apt/sources.list.d/vscodium.list
apt update && apt install codium
# use vscodium sandbox as default
rm /bin/codium-bin
mv /bin/codium /bin/codium-bin
touch /bin/codium
chmod +x /bin/codium
cat >/bin/codium <<EOF
#!/bin/bash
if [[ \$(id -u) -ne 0 ]]; then
  /bin/codium-bin $@
else
  /bin/codium-bin --no-sandbox $@
fi
EOF
```
### setup codeium

<!--TODO: ganti configs aja untuk path bin -->

hapus file `language_server_linux_arm` di folder `~/.codeium/bin/98dd1530ef0dce8888caa538e96fe193a7956819/` (jika random file lebih dari 1 maka hapus semua dulu), lalu buat file yang sama lalu paste code berikut :

> [!WARNING]
> mungkin nama folder akan berubah jika kita melakukan update. lakukan cara seperti ini, jika folder name berubah

```bash
#!/data/data/com.termux/files/usr/bin/bash

proot-distro login debian -- /root/.codeium/bin/<path>/language_server_linux_arm $@
```

> [!NOTE]
> ganti sesuai proot distro kalian, dan `<path>` diganti sesuai path kalian masing-masing
