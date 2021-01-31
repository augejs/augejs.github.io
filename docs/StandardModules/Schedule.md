---
id: Techniques-Schedule
title: Schedule
---

Task scheduling allows you to schedule arbitrary code (methods/functions) to execute with `cron` expressions which integrates with the popular [node-cron](https://github.com/kelektiv/node-cron) package. 


`cron` expressions

```bash
*    *    *    *    *    *
┬    ┬    ┬    ┬    ┬    ┬
│    │    │    │    │    |
│    │    │    │    │    └ day of week (0 - 7) (0 or 7 is Sun)
│    │    │    │    └───── month (1 - 12)
│    │    │    └────────── day of month (1 - 31)
│    │    └─────────────── hour (0 - 23)
│    └──────────────────── minute (0 - 59)
└───────────────────────── second (0 - 59, optional)
```

## Installation

To begin using it, we first install the required dependencies.


```bash
npm install --save @augejs/schedule
```

## Usage

```typescript
import { 
  Application, 
  Logger, 
  ILogger, 
  ConsoleLogTransport, 
  boot, 
  GetLogger, 
  Config} from '@augejs/module-core';

import { ScheduleModule, Schedule } from './main';

Logger.addTransport(new ConsoleLogTransport());

@Application({
  subModules: [
    ScheduleModule,
  ]
})
@Config({
  every5Sec: '*/5 * * * * *'
})
class AppModule {

  @GetLogger()
  logger!:ILogger;

  @Schedule('*/20 * * * * *')
  async every20Sec() {
    this.logger.info('every20Sec tick');
  }

  @Schedule(config => config.every5Sec)
  async every5SecFromConfig() {
    this.logger.info('every5SecFromConfig tick');
  }

  @Schedule(`*/4 * * * * *`)
  async every4SecWithLongTime() {
    await new Promise(resolve => {
      setTimeout(resolve, 8000);
    });
  }

  async onInit() {
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

export const Highlight = ({children, color}) => ( <span style={{
      backgroundColor: color,
      borderRadius: '2px',
      color: '#fff',
      padding: '0.2rem',
    }}>{children}</span> );

The <Highlight color="#25c2a0">@Schedule()</Highlight> decorator supports all standard [cron patterns](http://crontab.org/):

+ Asterisk (e.g. *)
+ Ranges (e.g. 1-3,5)
+ Steps (e.g. */2)