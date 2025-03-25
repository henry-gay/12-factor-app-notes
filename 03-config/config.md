# 03 - Config

## Summary
The **Config** factor of the 12-Factor App methodology emphasizes the separation of configuration from code. All configuration values (such as database URLs, credentials, and environment-specific settings) should be stored in environment variables, not in the codebase.

## Key Principles
1. **Store Config in Environment Variables**
   - Configuration should be stored in environment variables, which are set dynamically during runtime, not hardcoded in the code.
   - This enables different configurations for different environments (development, staging, production).

2. **Strict Separation of Config and Code**
   - Configuration should never be committed to source control. This ensures that sensitive data such as API keys or passwords is not exposed.

3. **Configuration as Environment-Specific**
   - Keep configuration values that vary between environments in environment variables, such as production database URLs, third-party service keys, etc.

4. **Use Defaults for Development**
   - For local development, use environment variable default values or tools like `.env` files (which should never be committed to source control).

## Best Practices
- Use libraries like `dotenv` (Node.js), `python-dotenv` (Python), or similar to load environment variables for local development.
- Ensure sensitive information such as credentials and API keys are securely stored in environment variables.
- Avoid hardcoding any configuration data in the codebase.
- Maintain different configurations for each environment (e.g., local, staging, production).

## Example

### Correct: Configuration in Environment Variables
```
DATABASE_URL=postgres://user:password@localhost/dbname
API_KEY=your-api-key
```

In your application code, read configuration values from environment variables:
```python
import os

database_url = os.getenv('DATABASE_URL')
api_key = os.getenv('API_KEY')
```

### Incorrect: Hardcoding Configuration in the Code
```python
# Don't hardcode values in the code
database_url = 'postgres://user:password@localhost/dbname'
api_key = 'your-api-key'
```

## Additional Resources
- [12factor.net - Config](https://12factor.net/config)
- [Python dotenv](https://pypi.org/project/python-dotenv/)
- [Node.js dotenv](https://www.npmjs.com/package/dotenv)
