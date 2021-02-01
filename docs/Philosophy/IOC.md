# [augejs](https://github.com/augejs/augejs.github.io)

[![npm version](https://badge.fury.io/js/%40augejs%2Fcore.svg)](https://www.npmjs.com/package/@augejs/core) [![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

<img height="100px" src="../assets/logo.svg">

[`augejs`](https://github.com/augejs/augejs.github.io) is a progressive Node.js framework for building applications.

:star2: Star us on GitHub — it helps! :clap:

https://github.com/augejs/augejs.github.io

## Inversion of control (IoC) container

Inversion of Control is a common phenomenon that you come across when extending frameworks. Indeed it's often seen as a defining characteristic of a framework.  --- [Martin Fowler](https://www.martinfowler.com/bliki/InversionOfControl.html)

`augejs` is on top of [InversifyJS](https://github.com/inversify/InversifyJS)

## Usage

```ts
import { Module, Inject } from '@augejs/core';
import { AXIOS_IDENTIFIER, AxiosInstance } from '@augejs/axios';
@Module()
class AppModule {
  @Inject(AXIOS_IDENTIFIER)
  httpService!: AxiosInstance;
}
```

We use the `@Inject` decorator to inject the instance.
