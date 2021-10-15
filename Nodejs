
### Source root/path for nodejs project. The easist and fastest way.

#### Typescript
``` 
declare global {
    namespace NodeJS {
        interface Global {
            __rootdir__: string;
        }
    }
}

#### Nodejs
``` 
global.__rootdir__ = __dirname || process.cwd();
```


