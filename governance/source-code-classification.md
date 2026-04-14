# Source Code Classification

## Classification Levels

| Level | Description | Examples |
|:---|:---|:---|
| **PUBLIC** | Safe for public repos | README.md, LICENSE, docs/ |
| **PRIVATE** | Internal logic, safe for org | src/*.ts, src/*.py |
| **SECRET** | Credentials, keys, tokens | .env, *.pem, auth.json |
| **LEAKABLE** | Accidentally exposed secrets | API keys, passwords |

## Rules

1. **NEVER** commit SECRET or LEAKABLE files
2. **NEVER** reference external source code (claude, anthropic, @ant/)
3. **ALWAYS** use environment variables for secrets
4. **ALWAYS** run `detect-secrets scan` before committing

## Enforcement

- Pre-commit hook blocks commits with external code references
- Pre-push hook blocks pushes with sensitive files
- CI workflow scans for leaked secrets
