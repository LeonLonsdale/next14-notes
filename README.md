# NextJS 14 Notes

Course notes based on learning through `Professional React and Next.JS` - a course produced by [ByteGrad.com](https://bytegrad.com).

# Contents

- [Installation and Setup](#installation-and-setup)
  - [Installation](#installation)
  - [Add Prettier for Tailwind and ESLint](#add-prettier-and-prettier-for-tailwind-and-eslint)
  - [Set project word wrapping and formatter](#enable-wordwrapping-and-set-default-formatter-in-vs-code)
- [Page Setup Basics](#page-setup-basics)
  - [Set page title and description](#set-page-title-and-description)
  - [Favicon](#favicon)
- [Route Management](#route-management)
  - [Create a Route](#create-a-route)
  - [Create a Dynamic Route](#create-a-dynamic-route)
  - [Get the current path](#get-the-current-pathname)
  - [Access the route](#access-the-route)
  - [Access the params](#access-the-params)
- [Security](#security)
  - [Cross-origin Sites](#cross-origin-sites)
    - [Images](#for-images)
- [Built-in NextJS Components](#built-in-nextjs-components)
  - [The Link component](#the-link-component)
  - [The Image Component](#the-image-component)

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

[Back to contents](#contents)

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

[Back to contents](#contents)

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

[Back to contents](#contents)

# Page Setup Basics

## Set page title and description

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

[Back to contents](#contents)

## Favicon

To set your favicon, just put it in the `./src/app/` directory.

[Back to contents](#contents)

# Route Management

## Create a Route

- Routes in NextJS work based on the folder structure
- The root path is `./src/app/`.
- The application homepage is `page.tsx` found in this directory.
- To create a new route, add a new directory in `.src/app/`.
- Each route must have its own `page.tsx`

```
.src/
    app/
        page.tsx
        news/
            page.tsx
        user/
            page.tsx
```

[Back to contents](#contents)

## Create a Dynamic Route

- A dynamic route is when the text in part of the path may vary
- Such as `/user/userId` where the userId will be different for each user.
- For a dynamic route we add a directory as before, but its name must be wrapped in square brackets.
- The page.tsx file must be in this directory.

```
.src/
    app/
        page.tsx
        news/
            page.tsx
        user/
            [id]
                page.tsx
```

[Back to contents](#contents)

## Custom 404 Not Found Response

- Handled by default but can be customised by creation of a special component.
- Create a file named `not-found.tsx` in the `app` dir
- Create a component in this file. It's used automatically.

```ts
export default function NotFound() {
  return <main>We could not find the page you are looking for.</main>;
}
```

[Back to contents](#contents)

## Get the current Pathname

- The pathname is the full path including the route, dynamic routes, queries etc.
- Accessible with a built inNextJS hook

```ts
import { usePathname } from "next/navigation";

const activePathname = usePathname();
```

[Back to contents](#contents)

## Access the Route

- We can access the route in object form using a built in nextjs hook.
- We can then manipulate this object to change the current route.

```ts
import { useRouter } from "next/navigation";

const router = useRouter();

// router now stored

router.push("route"); // go to pushed route.
```

[Back to contents](#contents)

## Access the Params

- Params are essentially what we represent with a dynamic route folder.
- We can access params using a built in NextJS Prop.
- `page.tsx` components get access to this prop by default.

```ts
type PageProps = {
    params: {
        id: string; // replace id with the dynamic route name
    }
};

export default Component({ params }: PageProps) { };
```

- In this example, `id` is the param name.
- This should match the dynamic route directory name.
- If the directory is `[city]` then replace `id` above with `city`.

[Back to contents](#contents)

# Security

## Cross-origin sites

- By default, NextJS blocks resources that are not locally accessible.
- To allow access to the resources we need, we have to edit the `next.config.js`.

### For Images

- Create an `image` property in the config file. This should be an object.
- Add an object property `remotePatterns` which should be an array.
- Add an object to the array with the properties `protocol` and `hostname`.
- Set the protocol value to `https` and the hostname value to the domain the image is sourced from.

```js
const nextConfig = {
  images: {
    remotePatterns: [{ protocol: "https", hostname: "bytegrad.com" }],
  },
};
```

[Back to contents](#contents)

# Built-in NextJS Components

## The Link component

- The link component creates `anchor` elements.
- Import it from `next/link`
- Accepts `href prop`
- Makes use of `children prop`.

```ts
import Link from "next/link";

<Link href="/">Home</Link>;
```

[Back to contents](#contents)

## The Image Component

- The Image component creates `img` elements.
- Import it from `next/image`
- Accepts `src`, `alt`, `width`, `height` props.
- Width and height props are only required for images that are sourced from a different domain.
- This is to reserve space for the image to avoid moving the UI around as things load.
- Locally sourced image dimensions are derrived automatically.

```ts
import Image from "next/image";

<Image src="" alt="" width={} height={} />;
```

[Back to contents](#contents)
