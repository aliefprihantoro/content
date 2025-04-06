# NeoVim: Editor Teks Modern untuk Pengembangan yang Efisien

**NeoVim**, atau **nvim**, adalah versi modern dari editor teks Vim yang terkenal. Dengan fokus pada peningkatan dan modernisasi, NeoVim menawarkan fitur-fitur baru seperti dukungan untuk plugin asinkron, Language Server Protocol (LSP), emulator terminal bawaan, manajemen paket bawaan, dan API yang lebih kuat.

## Instalasi NeoVim di Linux:

Untuk menginstal NeoVim di distribusi Linux, Anda dapat menggunakan manajer paket default. Namun, perlu diperhatikan bahwa versi yang diinstal mungkin bukan yang terbaru karena pembaruan paket yang tidak sering. Berikut adalah perintah untuk instalasi di beberapa distribusi populer:

- Termux:
  ```bash
  pkg install neovim
  ```
- Debian, Ubuntu, Linux Mint:
  ```bash
  sudo apt install neovim
  ```
- RHEL, Fedora, Alma Linux:
  ```bash
  sudo dnf install neovim
  ```
- Arch, Manjaro, EndeavourOS, Termux with pacman:
  ```bash
  sudo pacman -S neovim
  ```

Setelah instalasi, Anda dapat memverifikasi instalasi dengan perintah:

```bash
nvim -v
```

## install from scratch

1. prerequire

```bash
pkg install lua51 liblua53 liblua51 luajit libluajit luarocks luv lua-lpeg cmake make ninja clang luv libvterm libmsgpack libunibilium
luarocks install lpeg
luarocks install mpack
git clone https://github.com/neovim/neovim --depth=1
cd neovim
```

> [!IMPORTANT]
> kemungkinan ada pkg yang belum saya sertakan (pkg diatas sebenarnya tidak perlu diinstall). Jika terjadi error, silahkan kunjungi link berikut dan coba install satu persatu. [link prerequire](https://github.com/neovim/neovim/blob/v0.10.0/BUILD.md#build-prerequisites)

2. build
```bash
cmake -S cmake.deps -B .deps -G Ninja -D CMAKE_BUILD_TYPE=Release -DUSE_BUNDLED=OFF -DUSE_BUNDLED_LIBVTERM=ON -DUSE_BUNDLED_TS=ON
cmake --build .deps
make CMAKE_INSTALL_PREFIX=~/../usr CMAKE_BUILD_TYPE=Release install
```
> [!WARNING]
> If treesitter parsers are not bundled, they need to be available in a `parser/` runtime directory (e.g. `/usr/share/nvim/runtime/parser/`).

## Uninstall
```bash
cd ~/../usr
rm -rf lib/nvim share/nvim bin/nvim lib/lua/5.1/lpeg.so share/lua/5.1/re.lua share/applications/nvim.desktop share/icons/hicolor/128x128/apps/nvim.png
```
## Mode di Neovim

1. **Mode Normal**:

   - **Mode Normal** adalah mode utama di NeoVim. Di sini, Anda dapat melakukan perubahan pada teks, berpindah antar baris, dan mengoperasikan berbagai perintah.
   - Beberapa perintah dasar di mode normal:
     - **h**: Pindah ke kiri (sebagai pengganti panah kiri).
     - **j**: Pindah ke bawah (sebagai pengganti panah bawah).
     - **k**: Pindah ke atas (sebagai pengganti panah atas).
     - **l**: Pindah ke kanan (sebagai pengganti panah kanan).
     - **dd**: Menghapus baris saat ini.
     - **yy**: Menyalin baris saat ini.
     - **p**: Menyisipkan teks yang telah disalin.
     - **u**: Membatalkan perubahan terakhir.
     - **Ctrl + r**: Mengulangi perubahan yang dibatalkan.

2. **Mode Visual**:

   - **Mode Visual** memungkinkan Anda memilih teks secara visual sebelum melakukan operasi.
   - Cara masuk ke mode visual:
     - **v**: Mode visual karakter (pilih teks karakter per karakter).
     - **V**: Mode visual baris (pilih seluruh baris).
     - **Ctrl + v**: Mode visual blok (pilih area persegi panjang).

3. **Mode Insert**:

   - **Mode Insert** adalah mode di mana Anda dapat mengetik teks.
   - Masuk ke mode insert dengan menekan tombol **i** di mode normal.
   - Keluar dari mode insert dengan menekan tombol **Esc**.

4. **Mode Replace**:

   - **Mode Replace** memungkinkan Anda menggantikan karakter saat mengetik.
   - Masuk ke mode replace dengan menekan tombol **R** di mode normal.

5. **Perpindahan Vertikal dan Horizontal**:
   - Gunakan **h**, **j**, **k**, dan **l** untuk berpindah di mode normal.
   - **h** dan **l** untuk perpindahan horizontal (kiri dan kanan).
   - **j** dan **k** untuk perpindahan vertikal (atas dan bawah).

## Setup configs

Jika kalian membuka neovim pertamakali, pasti kalian kaget dengan tampilannya. Agar lebih cantik dan lebih produktif menggunakan termux, kalian bisa clone configurasi saya.
### install with my conf
```sh
mv ~/.config/nvim/ ~/.config/nvim.bak
git clone --depth 1 https://github.com/alifprihantoro/conf.nvim ~/.config/nvim
```
### install lsp
> [!IMPORTANT]
> ganti pnpm ke npm atau yarn jika kalian tidak menggunaksn pnpm.
> jika kamu tidak pakai termux silahkan ganti `pkg` menjadi package bawaan/bisa gunakan [mason](https://github.com/williamboman/mason.nvim)
> tutorial ini berfokus untuk termux yang mana tidak bisa memakai mason untuk instalasi
> hapus lsp/formatter yang tidak kalian butuhkan.

<!-- TODO: create mason registery, here for info : https://github.com/mason-org/mason-registry/blob/main/CONTRIBUTING.md#github-build-from-source -->
```sh
# setup neovim
pkg install luarocks luajit
luarocks install luacheck
# html,css,json, eslint
pnpm i -g vscode-langservers-extracted
# typescript compiler
pnpm i -g typescript                  
# lsp js/ts/tsx
pnpm i -g typescript-language-server  
# css module lsp
pnpm i -g cssmodules-language-server  
# astrojs lsp
pnpm i -g @astrojs/language-server    
# yaml lsp
pnpm i -g yaml-language-server        
# bash lsp
pnpm i -g bash-language-server        
pnpm i -g pyright
# tailwind lsp
pnpm i -g @tailwindcss/language-server
# mdx lsp
pnpm i -g @mdx-js/language-server     
# lsp lua
pkg install lua-language-server -y    
# lsp rust
git clone --depth=1 https://github.com/rust-lang/rust-analyzer.git
cd rust-analyzer
cargo xtask install --server
mv ~/.cargo/bin/rust-analyzer ~/../usr/bin/rust-analyzer
chmod 777 ~/../usr/bin/rust-analyzer
# php lsp
cd
curl -Lo phpactor.phar https://github.com/phpactor/phpactor/releases/latest/download/phpactor.phar
chmod a+x phpactor.phar
mv phpactor.phar ~/../usr/bin/phpactor
# lsp golang
go install golang.org/x/tools/gopls@latest
mv ~/go/bin/gopls ~/../usr/bin/

# install formatter
pkg install stylua -y # lua
pkg install shfmt -y  # bash
pnpm i -g @fsouza/prettierd  # formatter
echo '#!/bin/sh\necho "$(cat $1 | $PNPM_HOME/prettierd $1)"' >~/../usr/bin/astrofm
chmod +x ~/../usr/bin/astrofm

# go lsp linter
go install github.com/nametake/golangci-lint-langserver@latest
mv ~/go/bin/golangci-lint-langserver ~/../usr/bin/
# go linter
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
mv ~/go/bin/golangci-lint ~/../usr/bin/
```

Bagaimana, mulai tertarik? tulis di kolom komentar dibawah jika kalian rasa ada yang ingin kalian tahu. see you next time.

