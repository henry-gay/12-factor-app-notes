# 01 - Codebase

## Summary
The Codebase factor of the 12-Factor App methodology states that:
- A single codebase should be tracked in version control (e.g., Git).
- Multiple deploys (environments) should stem from the same codebase.
- There should never be multiple codebases for the same application.

## Key Principles
1. **One Codebase, Multiple Deploys**
   - The same codebase is used across development, staging, and production.
   - Different environments are handled through configuration, not separate codebases.

2. **Version Control as a Source of Truth**
   - Use Git, Mercurial, or another version control system to track code changes.
   - Every change should be committed and traceable.

3. **No Shared Codebase Between Multiple Apps**
   - If two applications share the same code, they should be combined into a single app or extracted into a dependency.

## Best Practices
- Use GitHub, GitLab, or Bitbucket for version control.
- Adopt a clear branching strategy, such as Git Flow or trunk-based development.
- Keep dependencies separate and not hardcoded in the codebase.
- Ensure CI/CD pipelines deploy from the same repository to maintain consistency.

## Example
### Correct: Single Codebase
```
my-app-repo/
│── .git/
│── src/
│── config/
│── tests/
│── README.md
```
### Incorrect: Separate Codebases for Environments
```
my-app-dev/
my-app-staging/
my-app-prod/
```

## Additional Resources
- [12factor.net - Codebase](https://12factor.net/codebase)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Trunk-Based Development](https://trunkbaseddevelopment.com/)