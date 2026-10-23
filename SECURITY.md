# Security Policy

[![Security policy](https://img.shields.io/badge/security-policy-0969da?style=flat-square&logo=github&logoColor=white)](https://github.com/osfv/BraveDebloater/security/policy)

Please report security-sensitive issues privately instead of opening a public issue. Use [GitHub private vulnerability reporting](https://github.com/osfv/BraveDebloater/security/advisories/new), or email [iqad@tersa.tech](mailto:iqad@tersa.tech) if you don't have a GitHub account. Please give us a chance to ship a fix before you disclose the issue publicly.

This project is intentionally conservative:

- It uses supported enterprise policies as the primary mechanism.
- It refuses known unsafe policy categories such as Shield disablement, Safe Browsing allowlists, TLS warning bypasses, and update disablement.
- It defaults to dry-run mode.
- It creates restore backups before applying changes.
- It validates backup metadata before restoring registry or profile files.

When reporting an issue, include the BraveDebloater version or commit, Windows version, Brave version, command used, and any relevant backup metadata with personal paths redacted.
