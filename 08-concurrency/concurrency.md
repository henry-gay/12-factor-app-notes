# 08 - Concurrency

## Summary
The **Concurrency** factor of the 12-Factor App methodology encourages scaling an application by running multiple instances of processes that are independent and stateless. It allows for handling increased traffic and load by adding more processes, without altering the application itself.

## Key Principles
1. **Scaling by Adding Processes**
   - Instead of relying on multi-threading or complex configurations within a single process, scale the application by running multiple instances of stateless processes that can handle different tasks or requests in parallel.

2. **Concurrency Through Process Model**
   - The application should handle multiple tasks by running several processes in parallel, each one handling a specific responsibility (e.g., web servers, background workers, cron jobs). These processes should be treated as first-class citizens, allowing for independent scaling.

3. **Independent Scaling**
   - Individual processes can be scaled independently based on their workload. For instance, the web server process can be scaled up to handle more HTTP requests, while background workers can be scaled independently to handle a queue of tasks.

4. **Concurrency Without Shared State**
   - Since processes are stateless, they do not share memory, and each process should store its state in a backing service (like a database or cache).

## Best Practices
- Use process orchestration tools (e.g., Kubernetes, Docker Compose) to manage scaling and handle process failures automatically.
- Consider using worker processes for long-running tasks or asynchronous jobs, separate from the web server process.
- Scale out based on traffic or resource demands, not by trying to scale a single process beyond its optimal capacity.
- Ensure the processes can run concurrently without depending on shared resources like memory or state.

## Example

### Correct: Running Multiple Web Processes and Worker Processes
- **Web Server Process**: Handles incoming HTTP requests.
- **Worker Process**: Handles background tasks, such as email processing, file uploads, etc.

```
# Running web server process
python manage.py runserver

# Running background worker process
python manage.py worker
```

### Incorrect: Overloading a Single Process with Multiple Responsibilities
```python
# Don't combine multiple responsibilities in a single process
# Example: Mixing web serving and background tasks in one process
def run():
    while True:
        handle_http_requests()  # Web server
        handle_background_tasks()  # Background jobs
```

## Additional Resources
- [12factor.net - Concurrency](https://12factor.net/concurrency)
- [Scaling with Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/)
- [Docker Compose for Multi-Process Applications](https://docs.docker.com/compose/)