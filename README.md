This is an example repro of a problem I encountered when trying to use react-flexbox-grid.

This repro is created by doing:
1. `create-razzle-app my-app`
2. `yarn add react-flexbox-grid`
3. Modify `src/Home.js` to use `Col` from `react-flexbox-grid`.

The error:

```
E:\web\src\my-app\node_modules\flexboxgrid2\flexboxgrid2.css:1
(function (exports, require, module, __filename, __dirname) { .container {
                                                              ^

SyntaxError: Unexpected token .
    at createScript (vm.js:80:10)
    at Object.runInThisContext (vm.js:139:10)
    at Module._compile (module.js:616:28)
    at Object.Module._extensions..js (module.js:663:10)
    at Module.load (module.js:565:32)
    at tryModuleLoad (module.js:505:12)
    at Function.Module._load (module.js:497:3)
    at Module.require (module.js:596:17)
    at require (internal/module.js:11:18)
    at Object.<anonymous> (E:\web\src\my-app\node_modules\react-flexbox-grid\lib\classNames.js:8:20)
```

Looks like the `react-flexbox-grid` `classNames.js` file is importing css. This is the contents:
```
'use strict';

Object.defineProperty(exports, "__esModule", {
  value: true
});
exports.default = getClass;

var _flexboxgrid = require('flexboxgrid2/flexboxgrid2.css');

var _flexboxgrid2 = _interopRequireDefault(_flexboxgrid);

function _interopRequireDefault(obj) { return obj && obj.__esModule ? obj : { default: obj }; }

function getClass(className) {
  return _flexboxgrid2.default && _flexboxgrid2.default[className] ? _flexboxgrid2.default[className] : className;
}
```

I don't know why this isn't working since razzle webpack should handle css imports.
