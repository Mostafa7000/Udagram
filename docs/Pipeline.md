# Pipeline process

The pipeline process is heavily dependent on the project npm scripts, and it starts there

## Step 1
- add install, build, test, and deploy scripts in the package.json of the frontend
- add install, build, and deploy scripts in the package.json of the backend
- ex. 
```
{
    "scripts": {
        "start": "node ./www/server.js",
        "tsc": "npx tsc",
        "dev": "npx ts-node-dev --respawn --transpile-only ./src/server.ts",
        "prod": "npx tsc && node ./www/server.js",
        "clean": "rm -rf www/ || true",
        "deploy": "npm run build && eb list && eb use Udacity-env && eb deploy",
        "build": "npm install . && npm run clean && tsc && cp -rf src/config www/config && cp -R .elasticbeanstalk www/.elasticbeanstalk && cp .npmrc www/.npmrc && cp package.json www/package.json && cd www && zip -r Archive.zip . && cd ..",
        "test": "echo \"Error: no test specified\" && exit 1"
    }
}
```

## Step 2
- add package.json file in the root folder containing both the bakend and frontend folders
- add scripts to navigate and trigger both the backend and frontend scripts you have just created
- ex.

```
{
    "scripts": {
        "frontend:install": "cd udagram/udagram-frontend && npm install -f",
        "frontend:start": "cd udagram/udagram-frontend && npm run start",
        "frontend:build": "cd udagram/udagram-frontend && npm run build",
        "frontend:test": "cd udagram/udagram-frontend && npm run test",
        "frontend:e2e": "cd udagram/udagram-frontend && npm run e2e",
        "frontend:lint": "cd udagram/udagram-frontend && npm run lint",
        "frontend:deploy": "cd udagram/udagram-frontend && npm run deploy",

        "api:install": "cd udagram/udagram-api && npm install .",
        "api:build": "cd udagram/udagram-api && npm run build",
        "api:start": "cd udagram/udagram-api && npm run dev",
        "api:deploy": "cd udagram/udagram-api && npm run deploy",
        
        "deploy": "npm run api:deploy && npm run frontend:deploy"
    }
}
```

## Step 3
- upload the project to a Github repo and use the repo in CircleCI
- configure the config.yml to contain the required scripts from the example above
- in the case of this project, the pipleine goes like this:
    1. Install node on the container
    2. Install Frontend Dependencies using command `npm run frontend:install`
    3. Install Backend Dependenciesnpm using command `npm run api:install`
    4. Linting the frontend using command `npm run frontend:lint`
    5. Build the frontend app using command `npm run frontend:build`
    6. Build the backend API using command `npm run api:build`
    7. Manually approving the deployment
    8. Installing eb cli and aws cli using orbs
    9. Deploying both the backend and the frontend using command `npm run deploy`
- Add all the needed secret keys to CircleCI enviroment variables so they can be used to setup your AWS account