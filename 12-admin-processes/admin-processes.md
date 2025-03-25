# 12 - Admin Processes

## Summary
The **Admin Processes** factor of the 12-Factor App methodology emphasizes the importance of treating administrative tasks (like database migrations, backups, or any one-off administrative jobs) as processes that run in the same environment as the app, but as separate, ephemeral processes.

## Key Principles
1. **Run Administrative Tasks as One-Off Processes**
   - Admin tasks should be executed as one-off processes, run explicitly by the user or as part of a CI/CD pipeline, rather than being integrated into the main application processes. These tasks should be run in the same environment (e.g., same dependencies, environment variables, etc.) as the application.

2. **Ephemeral and Disposable**
   - Admin processes should be treated as disposable and ephemeral. After the task completes, the process should terminate, and any resources used should be released.

3. **Consistency with Application Code**
   - Administrative tasks should run in an environment that matches the production environment as closely as possible. This ensures that the task's behavior matches what would occur in production and reduces the risk of issues due to environment discrepancies.

4. **Environment-Specific Administrative Processes**
   - Admin tasks, such as database migrations or seeding data, should be executed in the environment they affect, using the same configuration settings as the production application.

## Best Practices
- Run administrative tasks manually via CLI, or automate them via CI/CD pipelines.
- Ensure admin tasks are compatible with your app's environment, especially when interacting with backing services like databases.
- Use version-controlled scripts or tools to handle repetitive administrative tasks (e.g., migrations, backups).
- Don't mix admin tasks with normal application processes.

## Example

### Correct: Running Admin Tasks Separately
For example, running a database migration in a Python application:
```bash
# Run migration in the same environment as the app
python manage.py migrate
```

### Incorrect: Mixing Admin Processes with Application Logic
```python
# Don't mix application code and administrative tasks
def handle_user_signup():
    # Application logic
    pass

def run_migrations():
    # Admin process logic mixed with app logic
    pass
```

## Additional Resources
- [12factor.net - Admin Processes](https://12factor.net/admin-processes)
- [Flask Database Migrations](https://flask-migrate.readthedocs.io/en/latest/)
- [Django Database Migrations](https://docs.djangoproject.com/en/stable/migrations/)