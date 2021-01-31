# [augejs](https://github.com/augejs/augejs.github.io)

[![npm version](https://badge.fury.io/js/%40augejs%2Fcore.svg)](https://www.npmjs.com/package/@augejs/core) [![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

<img height="100px" src="../../docs/assets/logo.svg">

[`augejs`](https://github.com/augejs/augejs.github.io) is a progressive Node.js framework for building applications.

:star2: Star us on GitHub — it helps! :clap:

https://github.com/augejs/augejs.github.io

## Configuration

Applications often run in different environments.  Depending on the environment, different configuration settings should be used. `augejs` provides powerful and extensible configuration function.

### `Config` decorator configuration definition

```ts
import { Module, boot, Config } from '@augejs/core';

@Config({
  custom: {
    name: 'xxx',
    age: 111,
    detailInfo: {
      address: 'address xxxxxx'
    },
    friends: [
      {
        name: 'friends-001'
      }
    ]
  }
})
@Module
class AppModule {}
```

### FileConfig Decorator configuration definition

```ts
@YAMLConfig(path.join(process.cwd(), 'config/app.yml'))
@Module
class AppModule {}
```

### Command Line Parameters configuration definition

`augejs` use [yargs-parser](https://github.com/yargs/yargs-parser) for application command line configuration definition.

## Configuration definition priority

Command Line Parameters > FileConfig > Config

## Configuration Validation

We can use the `ConfigLoader` decorator to validate the configuration.

## Configuration Runtime Value

```ts
/**
 * Usage:
 * 
 * npm install @augejs/core reflect-metadata -S
 * 
 */

import { Module, boot, Config, Value } from '@augejs/core';

@Config({
  custom: {
    name: 'xxx',
    age: 111,
    detailInfo: {
      address: 'address xxxxxx'
    },
    friends: [
      {
        name: 'friends-001'
      }
    ]
  }
})
@Module()
class AppModule {

  // the value PropertyDecorator can get the global config value
  @Value()
  config!: any;

  // the value PropertyDecorator also support parameter
  @Value('custom')
  customConfig!: Record<string, any>;

  @Value('custom.name')
  customConfigName!: string;

  @Value('custom.detailInfo.address')
  customConfigAddress!: string;

  @Value('custom.friends.0.name')
  customConfigFirstFriendName!: string;

  async onInit() {
    // output custom config is { name: 'xxx', age: 111 }
    console.log('custom config is', this.config.custom);
    // output custom config is { name: 'xxx', age: 111 }
    console.log('custom config is', this.customConfig);
    // output: custom config name is xxx
    console.log('custom config name is', this.customConfigName);
    //output: custom config address is address xxxxxx
    console.log('custom config address is', this.customConfigAddress);
    // output: custom config first friend name is friends-001
    console.log('custom config first friend name is', this.customConfigFirstFriendName);
  }
}

(async () => {
  await boot(AppModule);
})();
```

https://github.com/augejs/examples/blob/master/packages/config/src/ymal-file-config.ts

