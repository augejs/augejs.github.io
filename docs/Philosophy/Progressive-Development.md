# [augejs](https://github.com/augejs/augejs.github.io)

[![npm version](https://badge.fury.io/js/%40augejs%2Fcore.svg)](https://www.npmjs.com/package/@augejs/core) [![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

<img height="100px" src="./docs/assets/logo.svg">

[`augejs`](https://github.com/augejs/augejs.github.io) is a progressive Node.js framework for building applications.

:star2: Star us on GitHub — it helps! :clap:

https://github.com/augejs/augejs.github.io

## Progressive Development

`augejs` application has the design philosophy of `Composition over inheritance`. The `augejs` core layer is small and simple. It supports the `Module`, `Provider`, `Decorator` to Composite the application.

### Webserver of Application

```ts
import { Module, boot } from '@augejs/core';
import { WebServer } from '@augejs/koa';

@WebServer()
@Module()
class AppModule {
  @RequestMapping.Get('ping')
  ping() {
    return 'pong';
  }
}

(async () => {
  await boot(AppModule);
})();
```

### Webserver(Koa) Application

```ts
import { Module, boot } from '@augejs/core';
import { WebServer } from '@augejs/koa';

@WebServer()
@Module()
class AppModule {
  @RequestMapping.Get('ping')
  ping() {
    return 'pong';
  }
}

(async () => {
  await boot(AppModule);
})();
```

https://github.com/augejs/examples/tree/master/packages/koa

### Spider Application

```ts
import { Module, ILogger, Inject, boot, GetLogger } from '@augejs/core';
import { AXIOS_IDENTIFIER, AxiosConfig, AxiosInstance } from '@augejs/axios';

@Module()
@AxiosConfig()
class AppModule {

  @Inject(AXIOS_IDENTIFIER)
  httpService!: AxiosInstance;

  @GetLogger()
  logger!: ILogger;

  async onInit() {
    this.logger.info('app on onInit');

    const results = await this.httpService.get('http://www.baidu.com');
    this.logger.info(results.data);
  }
}

async function main() {
  await boot(AppModule);
}

main();
```

https://github.com/augejs/examples/tree/master/packages/axios
