# Incident Response Playbook

## 🔴 Level 1: Secret Leak (CRITICAL)

### Immediate Actions (within 5 minutes)
1. **Revoke the leaked secret** immediately
2. **Force-push** to remove the commit from history
3. **Rotate all related credentials**

### Investigation (within 1 hour)
1. Check git history: `git log --all --full-history -- "**/*.env"`
2. Check GitHub Actions logs for exposed secrets
3. Check if secret was pushed to any forks

### Remediation (within 24 hours)
1. Update `.secrets.baseline` with new patterns
2. Update pre-commit hook with new detection rules
3. Create GitHub Issue documenting the incident

## 🟡 Level 2: External Code Reference (HIGH)

### Immediate Actions
1. Remove the reference: `git rm --cached <file>`
2. Replace with clean implementation
3. Commit with descriptive message

### Investigation
1. Search all files: `grep -r "claude\|anthropic\|@ant/" .`
2. Check git history for when reference was introduced

### Remediation
1. Update AGENTS.md with zero-external-code policy
2. Add lint rule to prevent future occurrences

## 🟢 Level 3: Minor Policy Violation (MEDIUM)

### Actions
1. Create GitHub Issue documenting the violation
2. Fix the violation in a new PR
3. Update relevant documentation

## Contact

- **Security Lead:** A2A-SIN-Security-Recon
- **Escalation:** A2A-SIN-Team-Infrastructure
- **Emergency:** Revoke all tokens via sin-authenticator
