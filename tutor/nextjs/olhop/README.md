# Pembuatan Web Online Shop

## rancangan

### teknologi

- next js
- storybook
- next auth
- firebase
- supabase
- eslint
- typescript
- prettier

### GOAL

- user dapat :
  - login
  - register
  - edit detail user
  - crud barang
  - mencari barang
  - membeli barang
  - menaruh item di keranjang
  - menerima notifikasi
  - mengetahui status barang

### Assumtion

- usr hanya bisa req api 1/s
- tidak ada data duplikat
- doble req :
  - disable btn after post
  - di colom db harus ada yang unik dan tidak auto generate seperti id, untuk cek apakah ada duplikasi (sku)
- error req :
  - mengembalikan array err
  - push to notify
- race condition :
  - user req bersamaan
- time out :
  - req usr diproses lama

### TODO

#### Setup

- next js
- eslint
- prettier
- tailwind
- firebase
- supabase
- storybook

#### FRONT END

- home
- login/register/reset password
- user detail
- keranjang
- payment
- status pesanan
-

#### BACK END

- auth
- user detail
- checkout
- payment
- status pesanan

#### QA

- wcag :
  - link
  - img
  - tabindex
  - color blind
- integration test :
  - login berhasil dan gagal
  - register belum ada usr dan sudah ada
- e2e test :
  - daftar
  - login
  - edit detail
  - beli barang
  - cek pesanan

## Praktek

### Setup project

#### setup next js :

```sh
pnpx create-next-app@latest
cd nama-folder
```

> pastikan sudah berjalan dengan lancar

#### setup storybook :

```sh
pnpm dlx storybook@latest init
```

#### setup eslint

- update versi 8

```sh
pnpm upgrade eslint
```

- bisa coba ikut configs saya :

```json
{
  "extends": [
    "next/core-web-vitals",
    "next/typescript",
    "plugin:storybook/recommended"
  ],
  "rules": {
    "comma-dangle": ["error", "always-multiline"],
    "prefer-template": ["error"],
    "no-multi-spaces": [
      "error",
      {
        "ignoreEOLComments": false
      }
    ],
    "no-multiple-empty-lines": [
      "error",
      {
        "max": 1
      }
    ],
    "no-trailing-spaces": ["error"],
    "no-mixed-spaces-and-tabs": ["error"],
    "camelcase": ["error"],
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "single"],
    "semi": ["error", "never"],
    "no-console": ["warn"],
    "no-alert": ["warn"]
  }
}
```

#### setup prettier

- add file `.prettierrc.yaml`
- write this :

```yaml
trailingComma: "all"
tabWidth: 2
semi: false
singleQuote: true
jsxSingleQuote: true
quoteProps: consistent
cursorOffset: -1
bracketSameLine: true
```

#### setup tailwind and daisy ui
- install daisyui
```sh
pnpm add -D daisyui@latest 
```
- edit `tailwind.config.ts`
```ts
import type { Config } from 'tailwindcss'
import daisyui from 'daisyui'
import themes from 'daisyui/src/theming/themes'

export default {
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      fontFamily: {
        Lato: ['Lato', 'sans-serif'],
        Rokkit: ['Rokkitt', 'serif'],
      },
      boxShadow: {
        center: '0 0 15px 3px blur',
      },
    },
  },
  daisyui: {
    themes: [
      {
        light: {
          ...themes['emerald'],
        },
      },
    ],
  },
  plugins: [daisyui],
} satisfies Config

```

#### setup github action
- add file `.github/workflows/test.yml`
```yml
name: "Lint and Chromatic"

on:
  pull_request:
    paths:
      - 'src/**/*.tsx'
      - 'src/**/*.stories.ts'

jobs:
  chromatic:
    name: Run Chromatic
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: Install pnpm
        uses: pnpm/action-setup@v4
        with:
          version: 9
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'pnpm'
      - name: Install dependencies
        run: pnpm install
      - name: lint
        run: pnpm lint
      - name: Run Chromatic
        uses: chromaui/action@latest
        with:
          # ⚠️ Make sure to configure a `CHROMATIC_PROJECT_TOKEN` repository secret
          projectToken: ${{ secrets.CHROMATIC_PROJECT_TOKEN }}
```
#### setup nextauth
- install `pnpm add next-auth`
- add file `src/app/api/auth/[...nextauth]/routes.ts`
```ts
import { authOptions } from "@/utils/authoptions";
import NextAuth from "next-auth/next";

const handler = NextAuth(authOptions);

export { handler as GET, handler as POST };

```
#### setup firebase
#### setup supabase

### Buat UI dengan Storybook

#### Nav/header

- link
- logo
- button user :
  - edit detail
  - login/logout
- button search
- btn keranjang

#### search

- input
- tags
- harga
- date
- list :
  - img
  - title
  - harga
  - qty

#### keranjang

- back/close
- list barang
- add/reduce qty
- delete list

#### heroes/slider/produk unggulan

#### Promo

#### Footer

#### Login/register/reset pass (auth)

#### detail barang

#### detail user/user setting

#### chat

####
