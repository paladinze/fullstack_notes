# Next: React server side rendering

## features
- webpack pre-configured
- performance optimization
- static html export

## installation
- mkdir next-ts
- cd next-ts
- npm init -y
- npm install --save react react-dom next
- mkdir pages
- modify package.json scripts
  - "dev": "next",
  - "build": "next build",
  - "start": "next start",
  - "export": "next export",

## special directory
- /pages
- /public

## layout
- patterns of reusable layout
  - props.children
  - higher order component
  - render props

## navigation
- client side use <Link>
- page routing
  - automatic based on filename in pages dir
- dynamic routing
  - query strings in <Link>
  - dynamic filenames: pages/p/[id].js

## fetch data for pages
- page implements getInitialProps
  - fetch inside getInitialProps
  - data available in props

## styling
- css file-based styling (avoid this in Next)
  - SASS
  - PostCSS
- CSS in Js (recomanded)
  - styled-jsx
    - component scoped css (no effect on child)

## API Routes
- lambdas (aka. serverless functions) running on Node
- every file inside page/api

## export as static html
- add next.config.js
- next build
- next export

## add typescript support
- npm install --save-dev typescript @types/react @types/node
- npm run dev

## build target: SSR vs static html
- most cases. add "target: serverless"
- getInitialProps => SSR
- SEO not important => don't SSR

## deployment
- deploy using now
  - npm i -g now
  - now