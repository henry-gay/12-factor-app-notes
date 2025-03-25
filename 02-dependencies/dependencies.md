# 02 - Dependencies

## Summary
The Dependencies factor of the 12-Factor App methodology emphasizes the explicit declaration and isolation of dependencies. Applications should not rely on system-wide packages but instead specify all dependencies in a manifest file and use a dependency manager.

## Key Principles
1. **Explicitly Declare Dependencies**
   - All dependencies must be listed in a dependency manifest file (e.g., `requirements.txt` for Python, `package.json` for Node.js, `go.mod` for Go).
   - The application should not assume that system-wide libraries are present.

2. **Use a Dependency Manager**
   - Dependency managers like Pip, NPM, or Bundler ensure that the correct versions of dependencies are installed.
   - A lockfile (e.g., `package-lock.json`, `Pipfile.lock`) should be used to maintain consistent dependency versions across different environments.

3. **Avoid Implicit Dependencies**
   - Never depend on system-wide packages that may vary between environments.
   - Ensure that all necessary libraries are installed as part of the application's setup process.

## Best Practices
- Use language-specific dependency managers to handle package installation.
- Keep dependencies up to date and monitor for security vulnerabilities.
- Use containerization (e.g., Docker) to isolate dependencies when necessary.
- Avoid global installations and ensure that dependencies are installed locally per project.

## Example
### Correct: Explicit Dependency Declaration
#### Python (`requirements.txt`)
```
Flask==2.0.1
requests==2.26.0
```
Install with:
```
pip install -r requirements.txt
```

#### Node.js (`package.json`)
```
{
  "dependencies": {
    "express": "^4.17.1",
    "axios": "^0.21.1"
  }
}
```
Install with:
```
npm install
```

### Incorrect: Implicit Dependency Usage
- Relying on a system-installed version of a library instead of specifying it in the manifest.
- Manually installing dependencies without tracking them in a version-controlled file.

## Additional Resources
- [12factor.net - Dependencies](https://12factor.net/dependencies)
- [Python Dependency Management](https://pip.pypa.io/en/stable/user_guide/)
- [Node.js Package Management](https://docs.npmjs.com/)