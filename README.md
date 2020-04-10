# simple-deploy-app-typescript-to-heroku

## Step 1. Making project root directory

```bash
mkdir simple-deploy-app-typescript-to-heroku
```

## Step 2. Initialize your directory as a node project

```bash
cd simple-deploy-app-typescript-to-heroku
npm init -y // automatic create new file package.json
```

## Step 3. Install required dependency using NPM

```bash
npm i @types/express @types/node express nodemon ts-node typescript
```

* Express is used for making REST API easier, also setting up a server is a very pleasant developer experience compare to normal Nodejs methods.
* Nodemon keeps the server running and swapping the latest code so we don't need to restart the server every time our update new code.
* ts-node directly runs .ts node file.
* typescript for type-script support to javascript.


## Step 4. Configuring Typescript

```bash
tsc --init // automatic for create new file tsconfig.json
```

Then add new line below <code>compilerOptions</code> object.

```json
"include" : [
    "src/**/*.ts"   /* Include every ts file in source folder */
],
"exclude" : [
    "node_modules"  /* exclude everything in  node_modules */
]
```

## Step 5. Setting up server

Edit file package.json

```json
"scripts": {
    "start": "ts-node src/config/server.ts", // 
    "dev": "nodemon -x ts-node src/config/server.ts"
},
```

> Server script would live in src/config/server.ts

Create new simple server with express now.

*src/config/server.ts*

```typescript
import express from 'express';
const app = express()
const PORT : string|number = process.env.PORT || 5000;

app.use("*",(req, res) =>{
    res.send("<h1>Welcome to your simple server! Awesome right</h1>");
});

app.listen(PORT,() => console.log(`hosting @${PORT}`));
```

Testing for server is running as well, we run cmd <code>npm run dev</code>.


## Step 6. Deploying to Heroku


### Substep 1: Installing [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)
### Substep 2: Logging in into Heroku

```bash
heroku login
```
Then we are going to new windows browser for login to Heroku application.

### Substep 3: Creating a heroku applicationx
### Substep 4: Creating a file Procfile for Heroku

Add new line to file
```bash
web:ts-node/src/config/server.ts
```

### Substep 5: Initializing our project into a git repo of Heroku

```bash
git init .
git add .
git commit -m "Initializing project"
```

### Finally of substeps: Pushing code to Heroku
```bash
git push heroku master
```