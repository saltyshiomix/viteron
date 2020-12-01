<p align="center">
  <a href="https://www.npmjs.com/package/viteron">
    <img src="https://img.shields.io/npm/v/viteron.svg">
  </a>
  <a href="https://www.npmjs.com/package/viteron">
    <img src="https://img.shields.io/npm/dt/viteron.svg">
  </a>
</p>

## viteron vs vite

| viteron | vite |
| --- | --- |
| `v0.x` | `v1.0.0-rc.x` |

## My Belief for viteron

1. Show a way of developing desktop apps only web knowledge
1. Easy to use
1. Be transparent and open to OSS developers

## Roadmaps

- [x] first implementation
- [x] [`create-viteron-app`](https://github.com/saltyshiomix/create-viteron-app)
- [ ] examples
  - [x] with-javascript
  - [ ] with-typescript
  - [ ] and more...
- [x] documentation (README)

## Usage

### Create Application with Template

We can use `examples/*` as a template.

To create the `examples/with-javascript`, run the command below:

```
# with npm
$ npm init viteron-app MY_APP --example with-javascript

# with yarn
$ yarn create viteron-app MY_APP --example with-javascript
```

### Run Electron with Development Mode

Run `npm run dev`, and viteron automatically launches an electron app.

```json
{
  "scripts": {
    "dev": "viteron"
  }
}
```

### Production Build

Run `npm run build`, and viteron outputs packaged bundles under the `dist` folder.

```json
{
  "scripts": {
    "build": "viteron build"
  }
}
```

### Build Options

To build Windows 32 bit version, run `npm run build:win32` like below:

```json
{
  "scripts": {
    "build": "viteron build",
    "build:all": "viteron build --all",
    "build:win32": "viteron build --win --ia32",
    "build:win64": "viteron build --win --x64",
    "build:mac": "viteron build --mac --x64",
    "build:linux": "viteron build --linux"
  }
}
```

**CAUTION**: To build macOS binary, your host machine must be macOS!

### Build Configuration

Edit `electron-builder.yml` properties for custom build configuration.

```yml
appId: com.example.viteron
productName: My Viteron App
copyright: Copyright © 2020 Shiono Yoshihide
directories:
  output: dist
  buildResources: resources
files:
  - from: .
    filter:
      - package.json
      - app
publish: null
```

For more information, please check out [electron-builder official configuration documents](https://www.electron.build/configuration/configuration).

## viteron.config.js

```js
module.exports = {
  // specify an alternate main src directory, defaults to 'main'
  mainSrcDir: 'main',
  // specify an alternate renderer src directory, defaults to 'renderer'
  rendererSrcDir: 'renderer',

  // main process' webpack config
  webpack: (defaultConfig, env) => {
    // do some stuff here
    return defaultConfig;
  },
};
```

### Additional Entries

```js
module.exports = {
  webpack: (defaultConfig, env) => Object.assign(defaultConfig, {
    entry: {
      // electron main process
      background: './main/background.js',
      // we can require `config.js` by using `require('electron').remote.require('./config')`
      config: './main/config.js',
    },
  }),
};
```

## Custom Babel Config

We can extends the default babel config of main process by putting `.babelrc` in our project root like this:

**`.babelrc`**:

```json
{
  "presets": [
    "viteron/babel"
  ]
}
```

## Examples

See [examples](./examples) folder for more information.

### [examples/with-javascript](./examples/with-javascript)

```
# with npm
$ npm init viteron-app my-app --example with-javascript

# with yarn
$ yarn create viteron-app my-app --example with-javascript
```

## Develop

### Basic

```
$ git clone https://github.com/saltyshiomix/viteron.git
$ cd viteron
$ yarn
$ yarn dev # default is examples/with-javascript
```

### Developing `examples/*`

```
$ yarn dev <EXAMPLE-FOLDER-NAME>
```

## Related

- [nextron](https://github.com/saltyshiomix/nextron) - ⚡ NEXT.js + Electron ⚡
- [nuxtron](https://github.com/saltyshiomix/nuxtron) - ⚡ Nuxt.js + Electron ⚡

## License

This project is licensed under the terms of the [MIT license](https://github.com/saltyshiomix/viteron/blob/main/LICENSE).
