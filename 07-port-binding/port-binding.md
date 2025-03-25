# 07 - Port Binding

## Summary
The **Port Binding** factor of the 12-Factor App methodology dictates that an application should expose its services via port binding. This means the application should not rely on a pre-configured web server or application server. Instead, it should run in an environment where it binds to a port, typically on a network interface, and is accessed via that port.

## Key Principles
1. **Self-Contained Web Services**
   - The application should export its web service via a specific port, allowing it to run independently without relying on external web servers. It should not depend on the underlying infrastructure or server setup to handle HTTP requests.

2. **Explicit Port Binding**
   - The application must bind to a specific port and listen for incoming HTTP requests. In cloud platforms, the assigned port should be available as an environment variable (e.g., `PORT`), allowing the app to run in any environment with ease.

3. **Environment Independence**
   - By binding to a specific port, the app becomes environment-independent and can run anywhere—on a local machine, cloud, or containerized environments—without changes to the codebase.

## Best Practices
- Use environment variables to configure the port the application binds to (e.g., `PORT=8080`).
- The application should be able to run on any available port, which can be dynamically assigned, especially in cloud or containerized environments.
- Do not hardcode any server configurations like ports into the application codebase.
- Port binding allows applications to be treated as self-contained units in modern cloud and containerized environments.

## Example

### Correct: Binding to a Port Dynamically
In a Node.js application:
```javascript
const express = require('express');
const app = express();
const port = process.env.PORT || 8080;

app.get('/', (req, res) => res.send('Hello World'));

app.listen(port, () => {
  console.log(`App listening at http://localhost:${port}`);
});
```

### Incorrect: Hardcoding the Port
```javascript
// Don't hardcode port
app.listen(8080, () => {
  console.log('App listening on port 8080');
});
```

## Additional Resources
- [12factor.net - Port Binding](https://12factor.net/port-binding)
- [Node.js HTTP Server](https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/)