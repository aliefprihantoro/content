## install
```sh
pnpm create astro@latest
cd ./app
```
```sh
pnpm astro add tailwind
pnpm add -D daisyui
pnpm add -D eslint eslint-plugin-lit eslint-plugin-lit-a11y eslint-plugin-wc
pnpm add @muryp/router-dom 
pnpm add -D @muryp/vite-html
pnpm astro add netlify
pnpm add firebase firebase-admin
```
## setup
### tailwindcss/daisyui
- add file on `src/assets/styles/main.css`
- paste :
```css
@import "tailwindcss";
@plugin "daisyui";
```

### vercel
### firebase
