# Readme

    ![license](https://img.shields.io/github/license/oslabs-beta/kafka-penguin?color=%2357d3af) ![issues](https://img.shields.io/github/issues-raw/oslabs-beta/kafka-penguin?color=yellow) ![last commit](https://img.shields.io/github/last-commit/oslabs-beta/kafka-penguin?color=%2357d3af) [![Repo stars](https://img.shields.io/github/stars/oslabs-beta/kafka-penguin?logoColor=%2334495e&style=social)](https://github.com/oslabs-beta/kafka-penguin/stargazers)

### About

kafka-penguin is an easy-to-use, lightweight kafkaJS plugin for message processing. It provides developers with two strategies for setting up message re-processing : Failfast and Dead Letter Queue.

#### For more information on kafkaJS, check out [Getting Started](https://kafka.js.org/docs/getting-started).

### Getting Started 

```bash
npm install kafka-penguin
```

Once installed it can now be referenced by simply calling `require('kafka-penguin');`

### Example

All kafka-penguin needs is a kafkaJS client to run. Start by passing the client for your preferred strategy and kafka-penguin will create bespoke consumers, producers, and admins with built-in functionality to execute the chosen strategy. On the surface, you implement your application exactly as you would with kafkaJS.

```javascript
import { FailFast } from 'kafka-penguin'
const exampleClient = require('./clientConfig.ts')

// Set up the preferred strategy with a configured KafkaJS client
const exampleStrategy = new FailFast(2, exampleClient)

// Initialize a producer or consumer from the instance of the strategy
const producer = exampleStrategy.producer();

const message = {
  topic: 'wrong-topic',
  messages: [
    {
      key: 'hello',
      value: 'world',
    }
  ]
}

// Connect, Subscribe, Send, or Run virtually the same as with KafkaJS
producer.connect()
  .then(() => console.log('Connected!'))
  // The chosen strategy executes under the hood, like in this send method
  .then(() => producer.send(message))
  .catch((e: any) => console.log('error: ', e.message))
```

### Strategies

#### FailFast

 Stop processing as soon as an error occurs. 

{% page-ref page="strategies/readme/strategies-readme-fail-fast.md" %}

#### DLQ

Handle message processing failures by forwarding problematic messages to a dead-letter queue \(DLQ\).

{% page-ref page="strategies/readme/strategies-readme-dlq.md" %}

## **Contributors**

[Ausar English](https://www.linkedin.com/in/ausarenglish) [@ausarenglish](https://github.com/ausarenglish)

Kushal Talele [@ktrane1](https://github.com/ktrane1)

[Timeo Williams](https://www.linkedin.com/in/timeowilliams/) [@timeowilliams](https://github.com/timeowilliams)

[Ziyad El Baz](https://www.linkedin.com/in/ziyadelbaz) [@zelbaz946](https://github.com/zelbaz946)

### License

This project is licensed under the Apache License - see the [LICENSE.md](https://github.com/oslabs-beta/kafka-penguin/blob/main/LICENSE) file for details.

