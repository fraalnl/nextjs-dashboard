# My notes on learning Next.js by following its official documentation

my node.js version is v.20

create vercel account connected to my github: https://vercel.com/new/rans-projects-f3ee58c9

using pnpm as your package manager
[right click `cmd`: run as Administrator]
`npm install -g pnpm@latest` 

But the next time to start: `win+x` => Terminal(Admin), the approach above that leads to system32 doesn't work

PowerShell has a security feature called "Execution Policy" that restricts the execution of scripts by default. 

`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`This command sets the execution policy to "RemoteSigned" for the current user, which means that only scripts downloaded from the internet that are signed by a trusted publisher can be run

# Chapter 1 created a Next.js application using the starter example and ran the development server

## 1) Create a Next.js app
In the project:

`/app`: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.

`/app/lib`: Contains functions used in your application, such as reusable utility functions and data fetching functions.

``/app/ui``: Contains all the UI components for your application, such as cards, tables, and forms. 

`/public`: Contains all the static assets for your application, such as images.

`Config Files`: config files such as next.config.js at the root of your application. 

`TypeScript`
- JavaScript is the core language of the web, and TypeScript is built upon it. Any valid JavaScript code is also valid TypeScript code.
- TypeScript adds features: static typing, classes, interfaces
- Static Typing: TypeScript lets you define the types of your variables and functions (e.g., number, string, boolean). This helps catch errors during development and makes your code more readable. JavaScript is dynamically typed, meaning it doesn't require you to specify types explicitly.
- Classes and Interfaces: TypeScript supports classes and interfaces, which provide object-oriented programming features.
- Compilation: TypeScript code needs to be compiled into JavaScript before it can be run in a browser or server. This process converts the TypeScript code into plain JavaScript, which the browser or server can understand.

Next.js detects if your project uses TypeScript and automatically installs the necessary packages and configuration

TSX stands for "TypeScript XML." It's a syntax extension used by TypeScript, which allows developers to write XML-like code that coexists with JavaScript/TypeScript code. This is especially common in frameworks like React, where components are often defined using a syntax that resembles HTML.

## 2) Running the development server
- run it `pnpm dev`
- localhost:3000

# Chapter 2 CSS
-You can import global.css in any component in your application, but it's usually good practice to add it to your top-level component. In Next.js, this is the root layout

- String-based className="": Use this for simple, static styles that don't require conditional logic. 
- Object-based className={{}}: Use this for dynamic styles that depend on variables, conditions, or other logic. 

``className={`${inter.className} mb-4 text-xl md:text-2xl`}``
- backticks (`) are used to create a template literal. embed variables and expressions directly within the string.
- inter.className variable holds a string of CSS classes applied elsewhere in your component
- The elements within the template literal (mb-4, text-xl, md:text-2xl) are likely Tailwind CSS class names.

    mb-4: Margin bottom of 4 units.

    text-xl: Text size "xl".

    md:text-2xl: Text size "2xl" for medium-sized screens (md).
- The resulting string is assigned to the className attribute, combining the styles from inter.className with the additional styles defined in the template literal.

e.g. inter.className has the value `font-bold text-gray-900`. The final className string would be:
`font-bold text-gray-900 mb-4 text-xl md:text-2xl`

## Tailwind: a CSS framework
When you use create-next-app to start a new project, Next.js will ask if you want to use Tailwind. If you select yes, Next.js will automatically install the necessary packages and configure Tailwind in your application.
## CSS Modules
CSS Modules allow you to scope CSS to a component by automatically creating unique class names, so you don't have to worry about style collisions as well.
## Using the clsx library to toggle class names
conditionally style an element based on state or some other condition.
Search for "clsx" in your code editor `Ctrl + Shift + F`, to find out what components use it to conditionally apply class names.

The clsx function is used to create dynamic class names in React
# Chapter 3 Optimizing Fonts and Images
Next.js can serve static assets, like images, under the top-level `/public` folder

The <Image> Component is an extension of the HTML <img> tag, and comes with automatic image optimization

when you use the block utility class, you're telling that element to behave like a paragraph or a heading: it will occupy the whole line by itself and push any following content to the next line.

`md:block`: The img element will be displayed as a block element on screens that are 768px wide or larger.
# Chapter 4 Creating Layouts and Pages
## Nested routing
Next.js uses file-system routing where folders are used to create nested routes. Each folder represents a route segment that maps to a URL segment.

create separate UIs for each route using `layout.tsx` and `page.tsx` files.

`/app/page.tsx` - this is the home page associated with the route /

create different pages in Next.js: create a new route segment using a folder, and add a page file inside it.

"colocate" refers to placing related code files together in the same location, usually within the same directory. This is in contrast to separating files by type (e.g., placing all stylesheets in one directory, all components in another, etc.).

only the contents returned by page.js or route.js are publicly addressable.

layout file is the best way to create a shared layout that all pages in your application can use.
# Chapter 5 Navigating Between Pages
`<Link>` allows you to do client-side navigation with JavaScript.

Client-Side Navigation: When you click a link with `<Link>`, Next.js only fetches the data needed for the new page and updates the content without reloading the entire page.

To use the `<Link />` component, open `/app/ui/dashboard/nav-links.tsx`, and import the Link component from `next/link`. Then, replace the `<a>` tag with `<Link>`

traditional React SPA, where the browser loads all your application code on initial load.

Splitting code by routes means that pages become isolated. If a certain page throws an error, the rest of the application will still work.

`usePathname` is a Client Component hook that lets you read the current URL's pathname.

By default, React Server Components are executed on the server, which can improve performance and SEO (Search Engine Optimization).

use the `client` directive when:

•	Using client-side APIs: If your component interacts with the browser's window, document, or other APIs, it needs to run on the client.

•	Implementing interactive UI elements: Components that rely on user input or updates, like forms, draggable elements, or animations, often require client-side execution.

•	Using third-party libraries that rely on client-side functionality: Some third-party libraries require browser features and must be run on the client.

The className attribute can be applied to any HTML element within your React component.
e.g. A div element: `<div className="my-container">...</div>`

`clsx`: classnames
# Chapter 6 Setting Up Your Database
By connecting your GitHub repository, whenever you push changes to your main branch, Vercel will automatically redeploy your application
## Create a Postgres database
On Vercel, create db -> copy secret to .env

run `pnpm i @vercel/postgres` in your terminal to install the `Vercel Postgres SDK`.

`/app/seed/route.ts` Next.js Route Handler. This creates a server-side endpoint that you can access in the browser to start populating your database.
# 7: Fetching Data
APIs are an intermediary layer between your application code and database.

you should not query your database directly when fetching data on the client as this would expose your database secrets.
## Using Server Components to fetch data
- Server Components support promises, providing a simpler solution for asynchronous tasks like data fetching. You can use `async/await` syntax without reaching out for `useEffect`, `useState` or data fetching libraries.
- Server Components execute on the server, so you can keep expensive data fetches and logic on the server and only send the result to the client.
- since Server Components execute on the server, you can query the database directly without an additional API layer.

## Fetching data for the dashboard overview page
- Named Exports = importing named exports, use curly braces {}.
- Default Exports = importing a module as a whole, you can use a default import without curly braces.
- Flexibility: Named imports allow you to import only the specific items you need, resulting in smaller bundle sizes and better code organization.