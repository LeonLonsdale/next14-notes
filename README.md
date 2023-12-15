# NextJS 14 Notes

# Contents

- [Installation and Setup](#installation-and-setup)
  - [Installation](#installation)
  - [Add Prettier for Tailwind and ESLint](#add-prettier-and-prettier-for-tailwind-and-eslint)
  - [Set project word wrapping and formatter](#enable-wordwrapping-and-set-default-formatter-in-vs-code)
- [Set page title and description](#set-page-title-and-description)

# Installation and Setup

## Installation

```bash
npx create-next-app@latest

Would you like to use TypeScript? 'Yes'
Would you like to use ESLint? 'Yes'
Would you like to use Tailwind CSS? 'Yes'
Would you like to use 'src/' directory? 'Yes'
Would you like to use App Router? 'Yes'
Would you like to customise the default import alias (@/*)? 'No'
```

## Add Prettier and Prettier for Tailwind and ESLint

```bash
npm i -D prettier prettier-plugin-tailwindcss
```

Create Prettier config

```bash
touch .prettierrc
```

Add tailwind css plugin to config

```json
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```

Let ESLint know about Prettier in `.eslintrc.json`

```json
{
  "extends": ["next/core-web-vitals", "prettier"]
}
```

## Enable WordWrapping and set default formatter in VS Code

1. Install the Prettier extension
2. Create a new folder in root `.vscode`
3. Inside create `settings.json`

```bash
mkdir .vscode
touch .vscode/settings.json
```

In the settings json, add

```json
{
  "editor.wordWrap": "wordWrapColumn",
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.wordWrapColumn": 80
}
```

# Set page title and description

- Access `./src/layout.tsx`
- Look for the `metadata` constant
- Edit object values as required

```ts
export const metadata: Metadata = {
  title: "Page title",
  description: "Page description",
};
```

- Different pages can have their own metadata constant export if required.
