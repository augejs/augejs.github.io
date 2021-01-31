# [augejs](https://github.com/augejs/augejs.github.io)

[![npm version](https://badge.fury.io/js/%40augejs%2Fcore.svg)](https://www.npmjs.com/package/@augejs/core) [![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

<img height="100px" src="./docs/assets/logo.svg">

[`augejs`](https://github.com/augejs/augejs.github.io) is a progressive Node.js framework for building applications.

:star2: Star us on GitHub — it helps! :clap:

https://github.com/augejs/augejs.github.io

## Table of Contents

- [Description](#description)
- [Features](#features)
- [Install](#install)
- [Usage](#usage)
- [Document](#document)
- [Examples](#Examples)
- [Related Efforts](#related-efforts)
- [Maintainers](#maintainers)
- [Contributing](#contributing)
- [License](#license)

## Description

`augejs` is a progressive Node.js framework for building applications. It uses modern JavaScript built with [TypeScript](http://www.typescriptlang.org/).

## Features

+ :penguin: Support TypeScript (version 4.0 or higher).
+ :shell: Minimum core to start with，support plugin by using Extend and Adapter.
+  :lollipop: ​Excellent performance with high unit test coverage rate.
+ :bread: Progressive Development.

## Install

This project uses [node](http://nodejs.org) and [npm](https://npmjs.com). Go check them out if you don't have them locally installed.

```sh
npm install @augejs/core
```

## Usage

```javascript
import { Module, boot } from '@augejs/core';

// we use a @Module decorator to define a module
@Module()
class AppModule {
  async onInit() {
    // the onInit lifecycle method will be called when application boot
    console.log('hello augejs');
  }
}

(async () => {
  // boot the whole application by module.
  await boot(AppModule);
})();
```

## Document

### Philosophy

+ [IOC](./docs/Philosophy/IOC.md)
+ [Application](./docs/Philosophy/Application.md)
+ [Boot](./docs/BasicFunction/boot.md)
+ [Hook](./docs/BasicFunction/Hook.md)
+ [Progressive Development](./docs/Philosophy/Progressive-Development.md)

### Basic Function

+ [Module](./docs/BasicFunction/Module.md)
+ [Provider](./docs/BasicFunction/Provider.md)
+ [ScanHook](./docs/BasicFunction/ScanHook.md)
+ [LifecycleHook](./docs/BasicFunction/LifecycleHook.md)
+ [Cluster](./docs/BasicFunction/Cluster.md)
+ [Config](./docs/BasicFunction/Config.md)
+ [Logger](./docs/BasicFunction/Logger.md)
+ [Name](./docs/BasicFunction/Name.md)
+ [Tag](./docs/BasicFunction/Tag.md)

### Standard Modules

+ [AMQP](./docs/StandardModules/AMQP.md)
+ [Axios](./docs/StandardModules/Axios.md)
+ [FileConfig](./docs/StandardModules/FileConfig.md)
+ [I18N](./docs/StandardModules/I18N.md)
+ [Koa](./docs/StandardModules/Koa.md)
+ [Log4js](./docs/StandardModules/Log4js.md)
+ [Mail](./docs/StandardModules/Mail.md)
+ [Redis](./docs/StandardModules/Redis.md)
+ [Schedule](./docs/StandardModules/Schedule.md)
+ [TypeOrm](./docs/StandardModules/TypeOrm.md)
+ [Views](./docs/StandardModules/Views.md)

### Koa-Modules

+ [Koa-bodyParser](./docs/StandardModules/Koa-bodyParser.md)
+ [Koa-compress](./docs/StandardModules/Koa-compress.md)
+ [Koa-error-handle](./docs/StandardModules/Koa-error-handle.md)
+ [Koa-multer](./docs/StandardModules/Koa-multer.md)
+ [Koa-security](./docs/StandardModules/Koa-security.md)
+ [Koa-session](./docs/StandardModules/Koa-session.md)
+ [Koa-static](./docs/StandardModules/Koa-static.md)

### Other-Modules

...

## :beers:Examples

see the [Examples](https://github.com/augejs/examples). :open_book:

## Related Efforts

- [Art of Readme](https://github.com/noffle/art-of-readme) - 💌 Learn the art of writing quality READMEs.
- [open-source-template](https://github.com/davidbgk/open-source-template/) - A README template to encourage open-source contributions.

## Maintainers

[Alex Zhang](https://github.com/alex-zhang).

## Contributing

Feel free to dive in! [Open an issue](https://github.com/augejs/core/issues) or submit PRs.

`augejs` follows the [Contributor Covenant](http://contributor-covenant.org/version/1/3/0/) Code of Conduct.

## License

[MIT](LICENSE) © augejs
