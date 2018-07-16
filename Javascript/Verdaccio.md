# Verdaccio
[verdaccio](http://www.verdaccio.org/) is a Lightweight private npm proxy registry

## Install
```shell=
npm install -g verdaccio
yarn global add verdaccio
```

## Usage

#### Simple to run the service
```shell=
verdaccio
```

#### Setup registry 
```
npm set registry http://localhost:4873
```

#### Register
```
npm adduser --registry http://localhost:4873
```

#### Login/logout
```
npm login(/logout)
```

#### Publish
```
npm publish --registry http://localhost:4873
```

#### unpublish
```
 npm unpublish -f
```

## [nrm -- NPM registry manager](https://github.com/Pana/nrm)
help you easy and fast switch between different npm registries


#### Install
```
npm install -g nrm
```

#### List all registry
```
nrm ls
```

#### Add
```
nrm add sbk-local http://localhost:4873
```

#### Use
```
nrm use sbk-local
```

