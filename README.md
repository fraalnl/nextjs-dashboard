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

By using `TypeScript`, you can ensure you don't accidentally pass the wrong data format to your components or database, like passing a string instead of a number to invoice amount.

Next.js detects if your project uses TypeScript and automatically installs the necessary packages and configuration

TSX stands for "TypeScript XML." It's a syntax extension used by TypeScript, which allows developers to write XML-like code that coexists with JavaScript/TypeScript code. This is especially common in frameworks like React, where components are often defined using a syntax that resembles HTML.

## 2) Running the development server
- run it `pnpm dev`
- localhost:3000

# Chapter 2 CSS
-You can import global.css in any component in your application, but it's usually good practice to add it to your top-level component. In Next.js, this is the root layout

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

use the use `client` directive when:

•	Using client-side APIs: If your component interacts with the browser's window, document, or other APIs, it needs to run on the client.

•	Implementing interactive UI elements: Components that rely on user input or updates, like forms, draggable elements, or animations, often require client-side execution.

•	Using third-party libraries that rely on client-side functionality: Some third-party libraries require browser features and must be run on the client.

The className attribute can be applied to any HTML element within your React component.
e.g. A div element: `<div className="my-container">...</div>`

`clsx`: classnames
# Chapter 6 Setting Up Your Database

