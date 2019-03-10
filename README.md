# mario-maker-project-v4

Yep. I'm at it again. ;P

## Goals

I'd like to achieve certain functional and technical goals with this project.

### Functional

### Technical

- linting (eslint)
- babel transpiling
- integration test against _built_ (transpiled) code
- annotate types, potentially generated using json schema somehow
- static (compile-time) and dynamic (runtime) **type-checking** (partial/opt-in)
    - `flow` & `flow-runtime` look promising
    
## Build-Setup Log

Here's what I'm doing to get the project set up with a build system.

Following [this babel guide](https://babeljs.io/docs/en/usage) and also [this one](https://flaviocopes.com/babel/):

```shell
npm install --save-dev @babel/core @babel/cli @babel/preset-env
npm install --save @babel/polyfill
```

```javascript
// babel.config.js
const presets = [
    [
        '@babel/preset-env', {
            'targets': {
                'node': '8.10.0'
            }
        }
    ]
];
module.exports = { presets };
```

.babelrc alternative
```json
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "node": "8.10.0"
        },
        "useBuiltIns": "usage"
      }
    ]
  ]
}
```

package.json script:
```json
{
  "scripts": {
    "build": "babel src --out-dir dist",
    "prebuild": "npm test"
  }
}
```

### Flow

Adding flow to the build process for type-checking.

Start with static type-checking (regular `flow`).

```shell
npm install --save-dev flow-bin @babel/preset-flow
```

package.json

```json
{
  "scripts": {
    "flow": "flow",
    "pretest": "npm run flow"
  }
}
```

```shell
npm flow init
```

then change the package.json "flow" script to `"flow": "flow check"`

.babelrc

```json
{
  "presets": [
    "@babel/preset-flow"
  ]
}
```

TODO: try out parcel as a replacement for directly using babel etc libs