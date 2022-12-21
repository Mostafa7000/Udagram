# Application dependancies

- Node v14.15.1 (LTS) or more recent.
- AWS CLI v2
- eb CLI
- npm 6.14.8 (LTS) or more recent
    - backend
        - typescript
        - express
        - aws-sdk
        - pg
        - jsonwebtoken
        - eslint
    - frontend
        - typescript
        - angular
        - ionic
        - zone.js
        - jasmine
        - mocha
        - tslint

*A more detailed look at the project dependencies can be found in package.json files for both the backend and frontend*

**Note: I had to add the option `"skipLibCheck": true` in tsconfig.json file to solve a problem resulting from two exact types existing in two different modules**