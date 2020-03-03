# deployment


## deploy static site: github pages
- install gh-pages
  ```sh
  npm install gh-pages --save-dev
  ```
- add script to package.json
  ```json
  // package.json
  "homepage": "http://<github_username>.github.io/<repo_name>",
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  }
  ```
- run scripts
  ```sh
  npm run predeploy
  npm run deploy
  ```