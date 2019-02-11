# storybook-issue-3843

This reproduces the issue described here: https://github.com/storybooks/storybook/issues/3843#issuecomment-460920059

## Steps to Reproduce

Run the following steps in a terminal of your choice:

```terminal
$ npx react-native init SBTest
$ cd SBTest
$ npx @storybook/cli sb init
$ yarn storybook
```

Ths results in the following configuration (check `yarn.lock` for more details):

Library | Version
------- | -------
react | 16.6.3
react-native | 0.58.4
@storybook/react-native | 4.1.11
@storybook/addon-actions | 4.1.11
@storybook/addon-links | 4.1.11
@storybook/addons | 4.1.11
@babel/core | 7.2.2
@babel/runtime | 7.3.1
babel-runtime | 6.26.0

## Expected result

Storybook starts without error

## Actual result

The following error:

```
tmp/SBTest git:(master) yarn storybook
yarn run v1.12.1
$ storybook start
=> Loading custom addons config.
=> Using default webpack setup based on "Create React App".

React Native Storybook started on => http://localhost:7007/

webpack built 4f01beca3a29904f15cc in 2596ms
✖ ｢wdm｣: Hash: 4f01beca3a29904f15cc
Version: webpack 4.29.3
Time: 2596ms
Built at: 02/11/2019 3:27:47 PM
                   Asset       Size   Chunks             Chunk Names
              index.html  700 bytes           [emitted]
static/manager.bundle.js   7.27 MiB  manager  [emitted]  manager
Entrypoint manager = static/manager.bundle.js
[0] multi ./storybook/addons.js ./node_modules/@storybook/react-native/dist/manager/index.js 40 bytes {manager} [built]
[./node_modules/@storybook/addons/dist/index.js] 4.23 KiB {manager} [built]
[./node_modules/@storybook/channel-websocket/dist/index.js] 3.13 KiB {manager} [built]
[./node_modules/@storybook/core-events/index.js] 493 bytes {manager} [built]
[./node_modules/@storybook/mantra-core/index.js] 41 bytes {manager} [built]
[./node_modules/@storybook/podda/dist/index.js] 4.06 KiB {manager} [built]
[./node_modules/@storybook/react-native/dist/manager/components/PreviewHelp.js] 2.44 KiB {manager} [built]
[./node_modules/@storybook/react-native/dist/manager/index.js] 467 bytes {manager} [built]
[./node_modules/@storybook/react-native/dist/manager/provider.js] 5.78 KiB {manager} [built]
[./node_modules/@storybook/ui/dist/compose.js] 763 bytes {manager} [built]
[./node_modules/@storybook/ui/dist/context.js] 309 bytes {manager} [built]
[./node_modules/@storybook/ui/dist/index.js] 3.52 KiB {manager} [built]
[./node_modules/@storybook/ui/dist/modules/api/index.js] 762 bytes {manager} [built]
[./node_modules/global/window.js] 232 bytes {manager} [built]
[./storybook/addons.js] 1.81 KiB {manager} [built] [failed] [1 error]
    + 639 hidden modules

ERROR in ./storybook/addons.js
Module build failed (from ./node_modules/babel-loader/lib/index.js):
Error: Plugin/Preset files are not allowed to export objects, only functions. In /Users/ullrich/tmp/SBTest/node_modules/babel-preset-react/lib/index.js
    at createDescriptor (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-descriptors.js:178:11)
    at items.map (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-descriptors.js:109:50)
    at Array.map (<anonymous>)
    at createDescriptors (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-descriptors.js:109:29)
    at createPresetDescriptors (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-descriptors.js:101:10)
    at passPerPreset (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-descriptors.js:58:96)
    at cachedFunction (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/caching.js:33:19)
    at presets.presets (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-descriptors.js:29:84)
    at mergeChainOpts (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-chain.js:320:26)
    at /Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-chain.js:283:7
    at buildRootChain (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/config-chain.js:68:29)
    at loadPrivatePartialConfig (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/partial.js:85:55)
    at Object.loadPartialConfig (/Users/ullrich/tmp/SBTest/node_modules/@babel/core/lib/config/partial.js:110:18)
    at Object.<anonymous> (/Users/ullrich/tmp/SBTest/node_modules/babel-loader/lib/index.js:140:26)
    at Generator.next (<anonymous>)
    at asyncGeneratorStep (/Users/ullrich/tmp/SBTest/node_modules/babel-loader/lib/index.js:3:103)
 @ multi ./storybook/addons.js ./node_modules/@storybook/react-native/dist/manager/index.js manager[0]
Child HtmlWebpackCompiler:
                          Asset      Size               Chunks  Chunk Names
    __child-HtmlWebpackPlugin_0  1.39 MiB  HtmlWebpackPlugin_0  HtmlWebpackPlugin_0
    Entrypoint HtmlWebpackPlugin_0 = __child-HtmlWebpackPlugin_0
    [./node_modules/html-webpack-plugin/lib/loader.js!./node_modules/@storybook/core/src/server/templates/index.ejs] 1.75 KiB {HtmlWebpackPlugin_0} [built]
    [./node_modules/lodash/lodash.js] 527 KiB {HtmlWebpackPlugin_0} [built]
    [./node_modules/webpack/buildin/global.js] (webpack)/buildin/global.js 472 bytes {HtmlWebpackPlugin_0} [built]
    [./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 497 bytes {HtmlWebpackPlugin_0} [built]
ℹ ｢wdm｣: Failed to compile.
```
