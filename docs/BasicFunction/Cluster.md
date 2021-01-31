# [augejs](https://github.com/augejs/augejs.github.io)

[![npm version](https://badge.fury.io/js/%40augejs%2Fcore.svg)](https://www.npmjs.com/package/@augejs/core) [![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

<img height="100px" src="../../docs/assets/logo.svg">

[`augejs`](https://github.com/augejs/augejs.github.io) is a progressive Node.js framework for building applications.

:star2: Star us on GitHub — it helps! :clap:

https://github.com/augejs/augejs.github.io

## Cluster

The Nodejs official solution provided by Node.js is Cluster module, and there's an introduction:

> A single instance of Node.js runs in a single thread. To take advantage of multi-core systems the user will sometimes want to launch a cluster of Node.js processes to handle the load.

> The cluster module allows you to easily create child processes that all share server ports.

+ the process that forks other processes is called Master process, it seems like a contractor that does nothing except forking other processes.

+ other forked processes are called Worker processes, as the name suggests, they are workers that work actually. They accept requests and provide services.

+ usually the number of Worker processes depends on the CPU core number, only in this way can we take full advantage of multi-core resources.

```javascript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  // Fork workers.
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', function(worker, code, signal) {
    console.log('worker ' + worker.process.pid + ' died');
  });
} else {
  // Workers can share any TCP connection
  // In this case it is an HTTP server
  http.createServer(function(req, res) {
    res.writeHead(200);
    res.end("hello world\n");
  }).listen(8000);
}
```

## `Cluster` decorator

```ts
import { 
  ILogger, 
  boot, 
  GetLogger, 
  Module,
  IScanNode,
  Cluster,
} from '@augejs/core';

import {
  WebServer,
  RequestMapping,
  } from '@augejs/koa';

@Cluster({
  workers: 2
}) 
@WebServer()
@Module()
class AppModule {

  @GetLogger()
  logger!:ILogger;

  @RequestMapping.Get()
  async api() {
    this.logger.info('api');
    return '----';
  }

  async onInit(scanNode: IScanNode) {
    this.logger.info('app on onInit');
  }

  async onAppWillReady() {
    this.logger.info('app on onAppWillReady');
  }

  async onAppDidReady() {
    this.logger.info('app on onAppDidReady');
  }
}

async function main() {
  await boot(AppModule);
}

main();
```
