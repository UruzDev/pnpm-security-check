# 🛡 PNPM + Socket.dev Security Check

This GitHub Action runs `pnpm audit` and `socket protect` to detect:
- Known vulnerabilities (`pnpm audit`)
- Suspicious or malicious packages (`Socket.dev`)
- Risky install scripts or obfuscated code

If issues are found, it:
- Comments the results on the pull request
- Fails the build to block merging

---

## 🚀 Usage

Add the following to your workflow (e.g. `.github/workflows/security-check.yml`):

```yaml
name: Security Check

on:
  pull_request:
    branches: [main]

jobs:
  audit:
    name: Run Security Audit
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write

    steps:
      - uses: actions/checkout@v3

      - uses: actions/setup-node@v3
        with:
          node-version: 20
          cache: 'pnpm'

      - uses: UruzDev/pnpm-security-check@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
