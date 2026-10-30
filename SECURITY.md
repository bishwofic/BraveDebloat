# Security Policy

Please report security-sensitive issues privately instead of opening a public issue. Use [GitHub private vulnerability reporting](https://github.com/bishwofic/BraveDebloat/security/advisories/new), and please allow time for a fix before disclosing publicly.

If the issue is in the script itself and also affects the original project, please report it to [osfv/BraveDebloater](https://github.com/osfv/BraveDebloater/security) too.

This project is intentionally conservative:

- It uses official Brave and Chromium enterprise policies only.
- It refuses unsafe policies such as disabling Shields, Safe Browsing allowlists, TLS warning bypasses and update disablement.
- The script previews by default and changes nothing without `-Apply`.
- It creates restore backups before applying changes, and validates them before restoring.
- The macOS profile and Windows `.reg` files are plain text, so every setting can be read before installing.

When reporting, include the commit you used, your OS and Brave version, the command or file you ran, and any relevant output with personal paths removed.
