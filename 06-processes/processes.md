# 06 - Processes

## Summary
The **Processes** factor of the 12-Factor App methodology advocates for the application to be executed as one or more stateless processes. These processes should be independent, with no reliance on shared memory or session state, allowing the app to scale efficiently.

## Key Principles
1. **Stateless Processes**
   - All processes should be stateless and share nothing. Any required state should be stored in a backing service (such as a database or cache).
   - Statelessness allows the application to scale horizontally by adding more process instances, without concerns about data consistency between instances.

2. **Processes as First-Class Citizens**
   - The application should be split into multiple processes, each responsible for a specific task (e.g., web server, background worker, scheduled task).
   - These processes should be lightweight and designed to run independently.

3. **Concurrency**
   - The app should be able to handle multiple processes running simultaneously. Horizontal scaling can be achieved by running more instances of processes in parallel (e.g., more web workers, background workers, etc.).

4. **Graceful Shutdown**
   - Processes should be able to handle termination gracefully, closing connections and releasing resources properly. They should be able to respond to termination signals like `SIGTERM` for clean shutdown.

## Best Practices
- Design your application to run multiple processes that handle different tasks (e.g., separate web workers, background jobs, etc.).
- Use a process supervisor or orchestration tool (like Docker, Kubernetes) to manage the lifecycle of processes.
- Ensure that processes do not store state in memory but instead use external backing services.
- Handle process failure gracefully, ensuring that new processes can be spun up quickly in case of failure.

## Example

### Correct: Stateless Web Server and Background Worker
- **Web Server Process**: Runs the web server to handle incoming HTTP requests.
- **Background Worker Process**: Processes jobs from a queue asynchronously.
- **Scheduled Tasks**: Runs cron jobs for periodic tasks (e.g., sending emails, cleaning up databases).

```
# Run the web server process
python manage.py runserver

# Run the background worker process
python manage.py worker
```

### Incorrect: Sharing State Between Processes
```python
# Don't store state between processes
# Example: Using memory to store state across processes
state = {}

def handle_request():
    state["session_id"] = "12345"  # This is not a stateless approach
```

## Additional Resources
- [12factor.net - Processes](https://12factor.net/processes)
- [Docker Process Management](https://docs.docker.com/config/containers/multi-container/)
- [Kubernetes Process Management](https://kubernetes.io/docs/concepts/workloads/pods/)