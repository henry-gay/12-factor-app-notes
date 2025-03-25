# 04 - Backing Services

## Summary
The **Backing Services** factor of the 12-Factor App methodology states that all services your application relies on (databases, caches, email services, etc.) should be treated as attached resources. These services should be accessed through external URLs or service discovery, rather than being embedded within the application.

## Key Principles
1. **Treat Backing Services as Attached Resources**
   - External services (such as databases, message queues, and caches) are connected to the application via URLs, API keys, or credentials, and they can be swapped or changed without impacting the application code.
   - The application should not embed these services but should access them via a defined interface.

2. **Use URLs to Connect to Backing Services**
   - Access to external services should be done through a URL or a service discovery mechanism. The environment variables that store these URLs should be configured in each environment (e.g., development, staging, production).

3. **Decouple Services from Application Code**
   - The application should be decoupled from its backing services. This allows services to be replaced with minimal changes to the application code.

4. **Scaling the Application and Services Independently**
   - Backing services should be independently scalable. The application can scale by adding more instances, and backing services can be scaled separately based on load.

## Best Practices
- Use environment variables to store service connection details (e.g., database URLs, API keys).
- Treat all external services, including storage, messaging queues, and caching, as backing services.
- Use service discovery or service brokers in cloud environments to manage connections to external services.
- Maintain versioned APIs for backing services to ensure compatibility when services change.

## Example

### Correct: Accessing Backing Services via Environment Variables
```
DATABASE_URL=postgres://user:password@localhost/dbname
REDIS_URL=redis://localhost:6379
```

In your application code, access these services via environment variables:
```python
import os

database_url = os.getenv('DATABASE_URL')
redis_url = os.getenv('REDIS_URL')
```

### Incorrect: Hardcoding Backing Service Details in Code
```python
# Don't hardcode service details
database_url = 'postgres://user:password@localhost/dbname'
redis_url = 'redis://localhost:6379'
```

## Additional Resources
- [12factor.net - Backing Services](https://12factor.net/backing-services)
- [Docker Compose](https://docs.docker.com/compose/)
- [Heroku Add-ons](https://devcenter.heroku.com/categories/add-ons)