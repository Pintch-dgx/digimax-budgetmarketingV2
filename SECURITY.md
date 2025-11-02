# Security Guidelines

## ⚠️ Important Security Practices

### Never Commit Sensitive Information

**Do NOT commit:**
- Passwords or credentials (even demo ones)
- API keys or tokens
- Private keys or certificates
- `.env` files with sensitive data
- Database files with real data

### Demo Credentials

For **demo and development purposes only**, credentials are documented in:
- `digimax-budget-marketing/docs/DEMO.md` - Complete demo guide with all test credentials

**Important**: These credentials are for **local development only** and should never be used in production.

### Production Credentials

For production deployments:
1. Use environment variables (`.env` files that are gitignored)
2. Use secure secret management services (Azure Key Vault, AWS Secrets Manager, etc.)
3. Rotate credentials regularly
4. Never share credentials via email, chat, or version control

### What to Do If Credentials Are Exposed

If credentials are accidentally committed:
1. **Immediately** rotate/change all exposed credentials
2. Remove the file from git history using `git filter-repo` or `BFG Repo-Cleaner`
3. Notify the team and security officer
4. Review access logs for unauthorized access

## Reporting Security Issues

If you discover a security vulnerability, please report it to:
- **Email**: security@digimax.example (update with real contact)
- **Do not** open a public GitHub issue for security vulnerabilities

## Development Best Practices

1. **Use `.env.local` for local secrets** - automatically gitignored by Next.js
2. **Use `.env.example`** for sharing required environment variable names (without values)
3. **Review commits** before pushing to ensure no sensitive data is included
4. **Enable pre-commit hooks** to scan for sensitive data

### Recommended `.env.local` Structure

```bash
# Authentication
AUTH_SECRET=your-generated-secret-here
NEXTAUTH_URL=http://localhost:3000

# Database
DATABASE_URL=file:./prisma/dev.db

# External APIs (if applicable)
# API_KEY=your-api-key-here
```

Generate a secure `AUTH_SECRET`:
```bash
openssl rand -base64 32
```

## Additional Resources

- [OWASP Security Practices](https://owasp.org/www-project-top-ten/)
- [Next.js Security Best Practices](https://nextjs.org/docs/app/building-your-application/configuring/environment-variables)
- [GitHub Secret Scanning](https://docs.github.com/en/code-security/secret-scanning)

---

**Last Updated**: 2025-11-02

