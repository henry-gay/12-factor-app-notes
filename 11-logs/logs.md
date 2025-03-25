# 11 - Logs

## Summary
The **Logs** factor of the 12-Factor App methodology states that an application should treat logs as event streams. Logs should not be stored or handled by the application itself, but instead be forwarded to a centralized logging service where they can be processed, analyzed, and retained for future use.

## Key Principles
1. **Treat Logs as Event Streams**
   - The application should generate logs as unbuffered event streams, outputting log entries to standard output (stdout) and standard error (stderr). These log entries should capture important events, errors, and debugging information from the application.

2. **Do Not Manage Logs**
   - The application should not concern itself with the storage or management of logs. Logs should be offloaded to a centralized logging service (e.g., cloud log management services, ELK stack, or third-party log aggregators) where they can be collected, stored, and analyzed.

3. **Logs Should Be Aggregated**
   - Logs from all application processes, services, and environments should be aggregated into one place, where they can be accessed and analyzed efficiently. This helps provide a full picture of the application's behavior.

4. **Centralized Log Management**
   - Using a centralized log management system ensures that logs can be searched, filtered, and visualized easily. Logs should be structured and timestamped to provide useful context for understanding application behavior.

## Best Practices
- Send logs to a centralized log management system (e.g., ELK stack, Splunk, or cloud services like AWS CloudWatch or Google Stackdriver).
- Ensure that logs are structured (e.g., in JSON format) for better analysis, querying, and filtering.
- Log only meaningful events—avoid excessive logging that could overwhelm log storage or obscure valuable insights.
- Use environment variables or logging configurations to control log levels (e.g., `DEBUG`, `INFO`, `ERROR`).

## Example

### Correct: Sending Logs to Standard Output
In Python, logs can be output to `stdout`:
```python
import logging
import sys

# Configure the logger
logger = logging.getLogger('app')
handler = logging.StreamHandler(sys.stdout)
formatter = logging.Formatter('%(asctime)s - %(message)s')
handler.setFormatter(formatter)
logger.addHandler(handler)
logger.setLevel(logging.INFO)

# Log an event
logger.info("Application started")
```

### Incorrect: Storing Logs Locally
```python
# Don't store logs locally inside the application
with open("app.log", "a") as log_file:
    log_file.write("Application started\n")
```

## Additional Resources
- [12factor.net - Logs](https://12factor.net/logs)
- [Elasticsearch, Logstash, Kibana (ELK Stack)](https://www.elastic.co/what-is/elk-stack)
- [Centralized Logging with Fluentd](https://www.fluentd.org/)