
### Root path for nodejs project. The easist and fastest way.

#### Typescript (in root file) index.ts
``` 
declare global {
    namespace NodeJS {
        interface Global {
            __rootdir__: string;
        }
    }
}

global.__rootdir__ = __dirname || process.cwd();
``` 

#### Nodejs (in root file) index.js
``` 
global.__rootdir__ = __dirname || process.cwd();
```


