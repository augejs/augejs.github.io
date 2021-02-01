# [augejs](https://github.com/augejs/augejs.github.io)

[![npm version](https://badge.fury.io/js/%40augejs%2Fcore.svg)](https://www.npmjs.com/package/@augejs/core) [![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

<img height="100px" src="../assets/logo.svg">

[`augejs`](https://github.com/augejs/augejs.github.io) is a progressive Node.js framework for building applications.

:star2: Star us on GitHub — it helps! :clap:

https://github.com/augejs/augejs.github.io

## Inversion of control (IoC) container

Inversion of Control is a common phenomenon that you come across when extending frameworks. Indeed it's often seen as a defining characteristic of a framework.  --- [Martin Fowler](https://www.martinfowler.com/bliki/InversionOfControl.html)

## Lifecycle of `Module` and `Provider`

### Instance method lifecycle hook

Both `Module` and `Provider` have the lifecycle method hook if it defined.

```javascript
import { Module, boot } from '@augejs/core';

@Module()
class AppModule {
  async onInit() {
    console.log('onInit');
  }

  async onAppWillReady() {
    console.log('onAppWillReady');
  }

  async onAppDidReady() {
    console.log('onAppDidReady');
  }

  async onAppWillClose() {
    console.log('onAppWillClose');
  }
}

(async () => {
  await boot(AppModule);
})();
```

`augejs` lifecycle mechanism is on top of [provider-scanner](https://github.com/augejs/provider-scanner#hookmetadata) hook which is middleware system.

[scan-execute-order](https://github.com/augejs/provider-scanner/raw/master/docs/assets/scan-execute-order.png)

### Decorator lifecycle hook

we can use `@LifecycleOnInitHook` , `@LifecycleOnAppWillReadyHook`, `@LifecycleOnAppDidReadyHook`, `@LifecycleOnAppWillCloseHook` decorator to class.

```ts
import { Module, boot } from '@augejs/core';

@Module()
@LifecycleOnInitHook(async (scanNode: IScanNode, next: Function) => {
  await new Promise((resolve: Function) => {
    setTimeout(()=>{
      logger.info('hook: LifecycleOnInitHook');
      resolve();
    }, 5000)
  })
  await next();
})
class AppModule {
  async onInit() {
    console.log('onInit');
  }

  async onAppWillReady() {
    console.log('onAppWillReady');
  }

  async onAppDidReady() {
    console.log('onAppDidReady');
  }

  async onAppWillClose() {
    console.log('onAppWillClose');
  }
}

(async () => {
  await boot(AppModule);
})();
```

We also can add many hook decorator in to one class and keep the execute order.

| Lifecycle hook method | Lifecycle event triggering the hook method call |
| - | - |
| `onInit` | The instance(`Module`, `Provider`) init hook method |
| `onAppWillReady` | The instance(`Module`, `Provider`) app will ready hook method, run once after all instances `onInit` |
| `onAppDidReady` | The instance(`Module`, `Provider`) app did ready hook hook method, run once after all instances `onAppWillReady` |
| `onAppWillClose` | The instance(`Module`, `Provider`) app will close hook hook method |
