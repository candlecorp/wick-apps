# Svelte + TS + Tailwind + Flowbite

This is the template I use for my projects. It's a combination of Svelte, TypeScript, TailwindCSS and Flowbite.
This gives the ability to make a UI with static files and works very well with wick hosted backends.

```bash
npm init vite
     //select svelte and typescript
     //cd into new directory
npm install
npx svelte-add@latest tailwindcss
pnpm i
pnpm i -D flowbite-svelte
```

Update tailwind.config.cjs to this

```javascript
/** @type {import('tailwindcss').Config}*/
const config = {
  content: [
    "./src/**/*.{html,js,svelte,ts}",
    "./node_modules/flowbite-svelte/**/*.{html,js,svelte,ts}",
  ],

  plugins: [require("flowbite/plugin")],

  darkMode: "class",

  theme: {
    extend: {
      colors: {
        // flowbite-svelte
        primary: {
          50: "#FFF5F2",
          100: "#FFF1EE",
          200: "#FFE4DE",
          300: "#FFD5CC",
          400: "#FFBCAD",
          500: "#FE795D",
          600: "#EF562F",
          700: "#EB4F27",
          800: "#CC4522",
          900: "#A5371B",
        },
      },
    },
  },
};

module.exports = config;
```
