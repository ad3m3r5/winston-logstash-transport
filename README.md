
# winston-logstash-transport

## Reference
 - Forked from: [https://github.com/liuyanjie/winston-logstash-transport](https://github.com/liuyanjie/winston-logstash-transport)
 - TCP support idea from: [https://github.com/staciewaleyko/winston-logstash-transport](https://github.com/staciewaleyko/winston-logstash-transport)

## Example

**Method 1 - Preferred**
```js
const logger = require('winston-logstash-transport').createLogger(null, {
    application: 'main-node-app',
    logstash: {host: '12.34.56.78', port: 12345, protocol: 'tcp'},
    transports: [
        new winston.transports.Console(),
    ]
})
```

**Method 2**
```js
const logger = winston.createLogger({
    level: 'info',
    format: winston.format.combine(
        winston.format.json(),
        winston.format.timestamp()
    ),
    transports: [
        new winston.transports.Console(),
        new LogstashTransport({host: '98.76.54.32', port: 54321, protocol: 'udp'})
    ]
})
```

## API

* `class LogstashTransport`

  * `options`
  * `options.host`, logstash host
  * `options.port`, logstash TCP/UDP port
  * `options.protocol`, logstash protocol (TCP/UDP) - defaults to TCP
  * `options.trailingLineFeed`, message trailing line feed (true/false) - necessary when using json_lines in logstash
  * `options.trailingLineFeedChar`, trailing char if trailingLineFeed == true
  * `options.silent`, null callback on log

* `createLogger()`

  * `application`, The name of application (allows you to specify in logstash filtering)
  * `hostname=os.hostname()`, The host where application run on.
  * `level='info'`, log level
  * `transports=[]`, others transports for winston
  * `logstash`, options for LogstashTransport (host/port/protocol/etc)
