# TypeScript and Next.js

## TypeScript

TypeScript is a programming language developed by Microsoft. It builds on
JavaScript with features such as static types, interfaces, and improved
editor tooling. TypeScript code is compiled to JavaScript so it can run in
JavaScript environments.

### Basic types

```ts
// Number
let age: number = 23;

// String
let user: string = "James";

// Boolean
let isStudent: boolean = true;

// Array
let marks: number[] = [1, 2, 3, 4, 5];
let names: Array<string> = ["Anu", "Manu"];

// Tuple: a fixed sequence of values with known types
let person: [string, number] = ["Anu", 21];

// Enum
enum Role {
  Admin,
  User,
  Guest,
}

let myRole: Role = Role.Admin;

// `any` allows values of different types, but reduces type safety.
let value: any = 10;
value = "Anu";
```

Prefer a specific type over `any` when possible so TypeScript can help catch
type-related mistakes.

### Functions

You can specify the types of a function's parameters and return value:

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

Use `?` to make a parameter optional. An optional parameter must come after
required parameters, and its value may be `undefined`:

```ts
function greet(name?: string): void {
  console.log(name);
}
```

# Next.js

## Overview

Next.js is a React framework developed by Vercel for building web
applications. It provides features for routing, rendering, and server-side
functionality that can help with performance and search engine optimization
(SEO).

## Key features

### Server-side rendering (SSR)

The server generates HTML for a page when it is requested and sends it to the
browser.

### Static site generation (SSG)

HTML is generated at build time and can be served to users afterward.

### File-based routing

Routes are created from files and folders in the app.

### Route handlers

Server-side endpoints can be added to a Next.js application.

### Rendering flexibility

Pages can use different rendering approaches, depending on the app's needs.

## Next.js vs. React

| Topic | Next.js | React |
|---|---|---|
| Rendering | Supports server-side rendering, static site generation, and client-side rendering. | Commonly used for client-side rendering; other approaches need additional setup. |
| Routing | Includes file-based routing. | Add a routing library or configure routing. |
| SEO | Server-rendered and static pages can help with SEO. | Server-rendered pages often need additional setup. |
| Backend features | Includes server-side features. | Usually paired with a separate backend for server-side features. |

## Create and run a project

### 1. Create a Next.js app

Open a terminal and run:

```bash
npx create-next-app@latest my-app
```

### 2. Start the development server

Move into the project folder and start the app:

```bash
cd my-app
npm run dev
```

### 3. Open the app

On the same computer, visit [http://localhost:3000](http://localhost:3000) in
your browser. If the terminal displays a different address, use that address.

## Common project files and folders

| File or folder | Purpose |
|---|---|
| `package.json` | Lists project metadata, dependencies, and npm scripts. |
| `tsconfig.json` | Configures TypeScript for the project. |
| `next.config.ts` | Configures Next.js options. This file may be named differently or omitted, depending on the project setup. |
| `next-env.d.ts` | Provides TypeScript declarations for Next.js types and features. |
| `app/` | The App Router directory. It contains route pages and layouts, and can define loading states, data fetching, and server components. |

## Routing in Next.js

The App Router uses file-based routing. A folder inside `app/` creates a URL
path segment, and a `page.tsx` file inside that folder defines the page for
that route. The root `app/page.tsx` file defines the home page.

For example, to create an `/about` page, add `app/about/page.tsx`:

```text
app/
├── page.tsx          # /
└── about/
    └── page.tsx      # /about
```

The folder name becomes the route segment. Add more nested folders to create
deeper routes, such as `app/blog/first-post/page.tsx` for `/blog/first-post`.

## Layouts

`layout.tsx` defines shared UI that appears across one or more pages. A layout
can include elements such as a navigation bar, footer, or container.

Layouts preserve their state and do not re-render when the user changes routes
within the layout.

## Server and client components

### Server components

Server components are the default in the App Router. They run on the server
and are suitable for:

- Database queries
- Backend logic
- Reading environment variables and secret keys
- Async operations and server-side data fetching

### Client components

Add `"use client"` to the top of a file to create a client component. Client
components are suitable for:

- State and component updates
- Event handlers
- Browser APIs
- Interactive UI

When a page needs both server and client behavior, a server component can
import a client component. Keep stateful and interactive code in client
components, and keep server-only logic in server components.

## Loading UI

Create a `loading.tsx` file to display a loading interface while Next.js waits
for a page or route segment to load.

```text
app/
├── loading.tsx
└── page.tsx
```

The loading UI can be a spinner, skeleton, progress indicator, or another
temporary component.

## Not-found UI

Create a `not-found.tsx` file to define the UI shown when a route or resource
cannot be found.

You can also call `notFound()` from `next/navigation` inside a server
component or route handler:

```tsx
import { notFound } from "next/navigation";

export default function Page() {
  // Show not-found UI when the resource is missing.
  notFound();
}
```

## Quick summary

- Use **React** to build user interfaces.
- Use **Next.js** when you want a React framework with built-in routing and
  multiple rendering options.