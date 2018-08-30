# ES6 and Design Patterns
## Creational Patterns
### Factory
Practically any function that returns an object without `new` keyword is a factory. An example is a mail template builder for nodemailer.
```javascript
const mailOptions = (options, component, props) => ({
    from: options.from,
    to: options.to,
    subject: options.subject,
    html: component && ReactDOMServer.renderToString(
      <div>
        <p>default template</p>
        <component {...props} />
      </div>
    )
})
```

### Singleton
Multiple objects that share the same instance. An example is building a logger in Node.js.
```javascript
class Logger {
  constructor() {
    this.logs = []
  }

  get count() {
    return this.logs.length
  }

  log(message) {
    const timestamp = new Date().toISOString()
    this.logs.push(`${timestamp}: ${message}`)
    return `${timestamp}: ${message}`
  }
}

class Singleton {
  constructor() {
    if (!this.instance) {
      this.instance = new Logger()
    }
  }

  getInstance() { 
    return this.instance
  }
}

const logger = new Singleton()

// both loggerA and B will share the same instance of logs
const loggerA = logger.getInstance()
const loggerB = logger.getInstance()

// however in node.js exporting the instantiation of Logger will be a singleton that can be imported
module.exports = new Logger()
```
