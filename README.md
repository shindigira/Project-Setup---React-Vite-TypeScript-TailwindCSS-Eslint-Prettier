## Project Setup - React, Vite, TypeScript, TailwindCSS, Eslint, Prettier

### Run these commands in a named project folder

```console
pnpm create vite my-react-app --template react-ts
pnpm add -D @types/node (path modules node)
pnpm add framer-motion react-anchor-link-smooth-scroll @heroicons/react
pnpm add -D @type/react-anchor-link-smooth-scroll
pnpm add -D tailwindcss postcss autoprefixer
pnpm tailwindcss init -p
```

- Follow the `TailwindCSS Init` walkthrough.

```console
pnpm add -D eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-airbnb-typescript eslint-plugin-react eslint-plugin-jest eslint-plugin-react-hooks eslint-plugin-import
pnpm add -D prettier prettier-plugin-tailwindcss eslint-config-prettier eslint-plugin-prettier
```

- Create an `.eslintrc.cjs` and include the following:

```js
module.exports = {
  env: {
    node: true,
    browser: true,
    es2021: true,
  },
  settings: {
    react: {
      version: "detect",
    },
  },
  parser: "@typescript-eslint/parser",
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
  },
  plugins: ["react", "react-hooks", "prettier", "@typescript-eslint"],
  extends: [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:prettier/recommended",
    "plugin:react/recommended",
    "plugin:react/jsx-runtime",
    "plugin:react-hooks/recommended",
  ],
  rules: {},
  globals: {
    Edit: "writable",
    console: "writable",
    _: "writable",
    $: "writable",
  },
};
```

- Modify the `prettier.config.cjs` with the following:

```js
module.exports = {
  tabWidth: 2,
  semi: true,
  singleQuote: false,
  trailingComma: "all",
  printWidth: 80,
  useTabs: false,
  endOfLine: "auto",
  plugins: [require("prettier-plugin-tailwindcss")],
};
```

- Add the below scripts to `package.json`:

```js
  "scripts": {
    ...,
    "lint:dry": "eslint ./src --ext .jsx,.js,.ts,.tsx --ignore-path ./.gitignore",
    "lint:fix": "eslint ./src --ext .jsx,.js,.ts,.tsx --quiet --fix --ignore-path ./.gitignore",
    "lint:format": "prettier  --loglevel warn --write \"./**/*.{js,jsx,ts,tsx,css,md,json}\" ",
    "lint": "yarn lint:format && yarn lint:fix ",
    "type-check": "tsc"
  }

```

- Add both a `.eslintignore` and a `.prettierignore` with the following:

```text
node_modules
.DS_Store
dist
dist-ssr
*.local
node_modules/*

```

- Add a `.vscode` directory with a file named `settings.json, include the following:

```js
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.formatOnPaste": false,
  // Runs Prettier, then ESLint
  "editor.codeActionsOnSave": ["source.formatDocument", "source.fixAll.eslint"]
}
```

- Modify the `.gitignore` to add `node_modules`

### Allow Absolute Pathing

- Modify `vite.config.ts` to allow absolute pathing from 'src'

```js
export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: [
      {
        find: "src",
        replacement: path.resolve(__dirname, "src"),
      },
    ],
  },
});
```

- Modify `tsconfig.json` to as well:

```js
{
  "compilerOptions": {
    "paths": {
      "src/*": ["./src/*"]
    },
    ...
}
```

- Follow the _Install Tailwind CSS with Vite_ instructions, create the `tailwind.config.cjs` and add the following:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {}, // Go to Tailwind on creating/extending custom tailwind classes
  },
  plugins: [],
};
```

- Add to `index.css`

```console
@tailwind base;
@tailwind components;
@tailwind utilities;
```

-

- Create `prettier.config.cjs` and include below:
- [Tailwind Sorting](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier#how-classes-are-sorted)

```js
module.exports = {
  plugins: [require("prettier-plugin-tailwindcss")],
};
```

### VSCode Extensions

- Prettier - Code formatter
- ES7+ React/Redux/React-Native
- Tailwind Documentation (CMD + CTRL + T)
- Tailwind CSS IntelliSense
- ESLint

## Optional Steps

- add Husky, Lint-Staged, Commitizen for setting up git commit hooks: (Git Commit Hook Guide)[https://medium.com/@imdavidrock/why-should-you-use-commitizen-husky-for-conventional-commit-and-have-unified-lint-41047aad6d]. Will intercept commits to force proper commits
- Use semantic git commit messages: [Git Commit Semantics](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716)

## Reference Materials

- Another's Project Setup (See `package.json`): [Forked Project](https://github.com/shindigira/vite-reactts-eslint-prettier?fbclid=IwAR2TH4lLqcTD_-3Pz7LcPfqRedhygCi8lllUrLukaUgDRa6OmKX1WhDTg68)
- Eslint Instructions: [ESLint Dev Article](https://dev.to/suchintan/reacttypescripteslint-prettier-full-setup-p7j?fbclid=IwAR2uN5_AzehtVsmuhuUbYyuofFyVSLipUlDdhUXwhbTAj50MFvS-d5m7Emo#Configure%20ESLint%20on%20the%20project)
- ESLint Config: [Best ESLint Config](https://brygrill.medium.com/create-react-app-with-typescript-eslint-prettier-and-github-actions-f3ce6a571c97)
