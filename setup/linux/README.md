## setup font
> pastikan jika tidak menggunakan font yang tidak sama dengan dibawah, gunakan nerd font agar icon tidak amburadul.
> jika ingin melihat list font gunakan `kitty list-fonts`
```sh
aria2c -x5 https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/FiraCode.zip
mkdir ~/.fonts
unzip FiraCode.zip firacode
mv firaCode /usr/share/fonts/truetype/
fc-cache -fv
```
## how add emoticon color (debian based)
- download font in [here](https://github.com/googlefonts/noto-emoji?tab=readme-ov-file)
```sh
mv <font>.ttf ~/.fonts
fc-cache -fv

```
## setup gtk themes :

- open [here](https://store.kde.org/)
- find theme you like, download (find in file tab), decompress into `$HOME/.themes`
- example my theme is [ojave](https://store.kde.org/p/1275087/)
- to decompress themes is `tar -xvf /path/to/file.tar.xz ~/.themes`
- type `lxappearance` then change themes on that gui
