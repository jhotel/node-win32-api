# win32-api

FFI Definitions of Windows win32 api for [node-ffi-napi]

[![GitHub tag](https://img.shields.io/github/tag/waitingsong/node-win32-api.svg)]()
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/badge/lang-TypeScript-blue.svg)
![Available platform](https://img.shields.io/badge/platform-win32-blue.svg)
[![Coverage Status](https://coveralls.io/repos/github/waitingsong/node-win32-api/badge.svg)](https://coveralls.io/github/waitingsong/node-win32-api)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)
[![lerna](https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg)](https://lernajs.io/)


## Initialization

```sh
npm run repo:init
```

## Packages

| Package       | Version                | Dependencies                 | DevDependencies                |
| ------------- | ---------------------- | ---------------------------- | ------------------------------ |
| [`win32-api`] | [![main-svg]][main-ch] | [![main-d-svg]][main-d-link] | [![main-dd-svg]][main-dd-link] |
| [`win32-def`] | [![def-svg]][def-ch]   | [![def-d-svg]][def-d-link]   | [![def-dd-svg]][def-dd-link]   |


## What can I do with this?
Calling win32 native functions come from user32.dll, kernel32.dll, comctl32.dll by Node.js via [node-ffi-napi]


## Installing
```sh
npm install win32-api
```


## Usage

### Find window and set window title
```ts
// **Find calc's hWnd, need running a calculator program manually at first**

/**
 * expose module:
 * C, Comctl32 for Comctl32 from lib/comctl32/api
 * K, Kernel32 for kernel32 from lib/kernel32/api
 * U, User32 for user32 from lib/user32/api
 */
import { K, U } from 'win32-api'
import * as ref from 'ref-napi'

const knl32 = K.load()
const user32 = U.load()  // load all apis defined in lib/{dll}/api from user32.dll
// const user32 = U.load(['FindWindowExW'])  // load only one api defined in lib/{dll}/api from user32.dll

const title = 'Calculator\0'    // null-terminated string
// const title = '计算器\0'    // string in chinese

const lpszWindow = Buffer.from(title, 'ucs2')
const hWnd = user32.FindWindowExW(null, null, null, lpszWindow)

if (hWnd && ! hWnd.isNull()) {
  // Caution: outputing hWnd will cuase exception in the following process, even next script!
  // NOT do below in the production code!
  // console.log('buf: ', hWnd); // avoid this
  console.log('buf: ', ref.address(hWnd)) // this is ok

  // Change title of the Calculator
  const res = user32.SetWindowTextW(hWnd, Buffer.from('Node-Calculator\0', 'ucs2'))

  if ( ! res) {
    console.log('SetWindowTextW failed')
  }
  else {
    console.log('window title changed')
  }
}
```

### [Ref](https://www.npmjs.com/package/ref-napi)
```ts
import { U } from 'win32-api'
import * as ref from 'ref-napi'

// so we can all agree that a buffer with the int value written
// to it could be represented as an "int *"
const buf  = Buffer.alloc(4)
buf.writeInt32LE(12345, 0)

const hex = ref.hexAddress(buf)
console.log(typeof hex)
console.log(hex)  // ← '7FA89D006FD8'

buf.type = ref.types.int  // @ts-ignore

// now we can dereference to get the "meaningful" value
console.log(ref.deref(buf))  // ← 12345
```

```ts
// usage of types and windef:
import { K, FModel as FM, DTypes as W } from 'win32-api'
import * as ref from 'ref-napi'

const knl32 = K.load()

const buf = Buffer.alloc(4) as FM.Buffer   // ← here the types
buf.writeInt32LE(12345, 0)

// const hInstance =<FM.Buffer> Buffer.alloc(process.arch === 'x64' ? 8 : 4)
const hInstance = ref.alloc(W.HINSTANCE) as FM.Buffer    // W.HINSTANCE is 'int64*' under x64, 'int32*' under ia32
knl32.GetModuleHandleExW(0, null, hInstance)
```

### [Struct](https://www.npmjs.com/package/ref-struct)
```ts
// struct usage with ref-struct
import * as Struct from 'ref-struct'
import { DModel as M, DStruct as DS } from 'win32-api'

// https://msdn.microsoft.com/en-us/library/windows/desktop/dd162805(v=vs.85).aspx
const point: M.POINT_Struct = new Struct(DS.POINT)()
point.x = 100
point.y = 200
console.log(point)

// struct usage with ref-struct-di
import * as ref from 'ref-napi'
import * as StructDi from 'ref-struct-di'
import { DModel as M, DStruct as DS } from 'win32-api'

const Struct = StructDi(ref)
const point: M.POINT_Struct = new Struct(DS.POINT)()
point.x = 100
point.y = 200
console.log(point)
```

### Async Find window and set window title
```ts
// **Find calc's hWnd, need running a calculator program manually at first**

import { U } from 'win32-api'
import * as ref from 'ref-napi'


const u32 = U.load(['FindWindowExW', 'SetWindowTextW'])
const lpszClass = Buffer.from('CalcFrame\0', 'ucs2')

u32.FindWindowExW.async(null, null, lpszClass, null, (err, hWnd) => {
  if (err) {
    throw err
  }

  if (hWnd && !ref.isNull(hWnd) && ref.address(hWnd)) {
    const title = 'Node-Calculator'
    // Change title of the Calculator
    u32.SetWindowTextW.async(hWnd, Buffer.from(title + '\0', 'ucs2'), err2 => {
      if (err2) {
        throw err2
      }

      const buf = Buffer.alloc(title.length * 2)
      u32.GetWindowTextW.async(hWnd, buf, buf.byteLength, err3 => {
        if (err3) {
          throw err3
        }

        const str = buf.toString('ucs2').replace(/\0+$/, '')
        if (str !== title) {
          throw new Error(`title should be changed to ${title}, bug got ${str}`)
        }
      })
    })
  }
  else {
    throw new Error('FindWindowExW() failed')
  }
})
```


## Demo
- [create_window](https://github.com/waitingsong/node-win32-api/blob/master/packages/win32-api/demo/create_window.ts)
- [More](https://github.com/waitingsong/node-win32-api/blob/master/packages/win32-api/test)


## Dependencies Troubleshooting

Compile successfully with
  - Node.js v12 and Python v3.7
  - Node.js v10 and Python v2.7

If installation of node-gyp fails:
Check out [node-gyp] and [windows-build-tools]


## Relevant
- [Windows Api documentation](https://msdn.microsoft.com/en-us/library/windows/desktop/ff468919%28v=vs.85%29.aspx)
- [Windows Data Types](https://msdn.microsoft.com/en-us/library/windows/desktop/aa383751#DWORD)
- [System Error Codes](https://msdn.microsoft.com/en-us/library/windows/desktop/ms681381%28v=vs.85%29.aspx)
- [FFI doc](https://github.com/node-ffi/node-ffi/wiki/Node-FFI-Tutorial)
- [ref doc](https://tootallnate.github.io/ref/)
- [ref-struct](https://github.com/TooTallNate/ref-struct)


## License
[MIT](LICENSE)


### Languages
- [English](README.md)
- [中文](README.zh-CN.md)


[node-gyp]: https://github.com/nodejs/node-gyp
[windows-build-tools]: https://github.com/felixrieseberg/windows-build-tools
[node-ffi-napi]: https://github.com/node-ffi-napi/node-ffi-napi
[node-ffi]: https://github.com/node-ffi/node-ffi

[`win32-api`]: https://github.com/waitingsong/node-win32-api/tree/master/packages/win32-api
[main-svg]: https://img.shields.io/npm/v/win32-api.svg?maxAge=86400
[main-ch]: https://github.com/waitingsong/node-win32-api/tree/master/packages/win32-api/CHANGELOG.md
[main-d-svg]: https://david-dm.org/waitingsong/node-win32-api.svg?path=packages/win32-api
[main-d-link]: https://david-dm.org/waitingsong/node-win32-api.svg?path=packages/win32-api
[main-dd-svg]: https://david-dm.org/waitingsong/node-win32-api/dev-status.svg?path=packages/win32-api
[main-dd-link]: https://david-dm.org/waitingsong/node-win32-api?path=packages/win32-api#info=devDependencies

[`win32-def`]: https://github.com/waitingsong/node-win32-api/tree/master/packages/win32-def
[def-svg]: https://img.shields.io/npm/v/win32-def.svg?maxAge=86400
[def-ch]: https://github.com/waitingsong/node-win32-api/tree/master/packages/win32-def/CHANGELOG.md
[def-d-svg]: https://david-dm.org/waitingsong/node-win32-api.svg?path=packages/win32-def
[def-d-link]: https://david-dm.org/waitingsong/node-win32-api.svg?path=packages/win32-def
[def-dd-svg]: https://david-dm.org/waitingsong/node-win32-api/dev-status.svg?path=packages/win32-def
[def-dd-link]: https://david-dm.org/waitingsong/node-win32-api?path=packages/win32-def#info=devDependencies
