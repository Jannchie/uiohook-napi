# uiohook-napi

```bash
npm i @jannchie/uiohook-napi
```

Fixed an issue where the package path could not be located due to execution path changes when using WebPack packaging. Specific performance is as follows:

```
Error: No native build was found for platform=win32 arch=x64 runtime=electron abi=106 uv=1 libc=glibc node=16.14.2 electron=19.0.4 webpack=true
    loaded from: xxxxxx\uiohook-napi

    at load.path (xxxxxx\.webpack\main\index.js:26432:9)
    at load (xxxxxx\.webpack\main\index.js:26408:30)
    at ./node_modules/.pnpm/uiohook-napi@1.2.0/node_modules/uiohook-napi/dist/index.js (xxxxxx\.webpack\main\index.js:36148:136)
    at __webpack_require__ (xxxxxx\.webpack\main\index.js:76498:42)
    at xxxxxx\.webpack\main\index.js:76584:5
    at xxxxxx\.webpack\main\index.js:76795:3
    at Object.<anonymous> (xxxxxx\.webpack\main\index.js:76798:12)
    at Module._compile (node:internal/modules/cjs/loader:1118:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1173:10)
    at Module.load (node:internal/modules/cjs/loader:988:32)
```

[![](https://img.shields.io/npm/v/uiohook-napi/latest?color=CC3534&label=uiohook-napi&logo=npm&labelColor=212121)](https://www.npmjs.com/package/uiohook-napi)


N-API C-bindings for [libuiohook](https://github.com/kwhat/libuiohook).


### Usage example

```typescript
import { uIOhook, UiohookKey } from 'uiohook-napi'

uIOhook.on('keydown', (e) => {
  if (e.keycode === UiohookKey.Q) {
    console.log('Hello!')
  }

  if (e.keycode === UiohookKey.Escape) {
    process.exit(0)
  }
})

uIOhook.start()
```

### API

```typescript
interface UiohookNapi {
  on(event: 'input', listener: (e: UiohookKeyboardEvent | UiohookMouseEvent | UiohookWheelEvent) => void): this

  on(event: 'keydown', listener: (e: UiohookKeyboardEvent) => void): this
  on(event: 'keyup', listener: (e: UiohookKeyboardEvent) => void): this

  on(event: 'mousedown', listener: (e: UiohookMouseEvent) => void): this
  on(event: 'mouseup', listener: (e: UiohookMouseEvent) => void): this
  on(event: 'mousemove', listener: (e: UiohookMouseEvent) => void): this
  on(event: 'click', listener: (e: UiohookMouseEvent) => void): this

  on(event: 'wheel', listener: (e: UiohookWheelEvent) => void): this
}

export interface UiohookKeyboardEvent {
  altKey: boolean
  ctrlKey: boolean
  metaKey: boolean
  shiftKey: boolean
  keycode: number
}

export interface UiohookMouseEvent {
  altKey: boolean
  ctrlKey: boolean
  metaKey: boolean
  shiftKey: boolean
  x: number
  y: number
  button: unknown
  clicks: number
}

export interface UiohookWheelEvent {
  altKey: boolean
  ctrlKey: boolean
  metaKey: boolean
  shiftKey: boolean
  x: number
  y: number
  clicks: number
  amount: number
  direction: WheelDirection
  rotation: number
}
```
