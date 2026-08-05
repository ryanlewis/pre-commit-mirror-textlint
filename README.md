# textlint pre-commit hook

> [!CAUTION]
> **This repository is archived and no longer maintained** (August 2026).
>
> **Why:** pre-commit's `language: node` hooks resolve transitive npm dependencies live at
> install time — only the top-level package is pinned. During the 4 August 2026
> keyv/cacheable supply-chain attack, a fully pinned `textlint` hook from this mirror could
> still install the malicious `cacheable@2.5.1` through the floating chain
> `textlint → file-entry-cache → flat-cache → cacheable`. Pinning a `rev:` here never
> protected you from that, and pre-commit has no lockfile mechanism to fix it
> ([pre-commit#1963](https://github.com/pre-commit/pre-commit/issues/1963)).
>
> **What to do instead:** run textlint from a `package.json` governed by a committed
> `package-lock.json` (`npm ci`), via your CI or a hook manager that uses your project's
> lockfile. Additionally consider `min-release-age=7` and `ignore-scripts=true` in `.npmrc`
> (npm ≥ 11.10).
>
> Existing tags remain usable but frozen — no further textlint versions will be mirrored.

This repository provides [textlint](https://github.com/textlint/textlint) as a [pre-commit](https://pre-commit.com/) hook.

## About textlint

textlint is a pluggable linter for natural language text that helps catch writing issues in markdown and plain text files. It's similar to ESLint but designed for prose rather than code.

## Usage

Add this to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/ryanlewis/pre-commit-mirror-textlint
    rev: v15.1.0  # Use the ref you want to point at
    hooks:
      - id: textlint
```

By default, this hook runs on markdown files. You can configure it to run on additional file types:

```yaml
repos:
  - repo: https://github.com/ryanlewis/pre-commit-mirror-textlint
    rev: v15.1.0
    hooks:
      - id: textlint
        types: [markdown, text]
```

## Configuration

textlint requires rules to be effective. There are two ways to configure textlint rules:

### Option 1: NPM Dependencies (Traditional Method)

Create a `.textlintrc` file in your repository root:

```json
{
  "rules": {
    "@textlint-rule/textlint-rule-no-unmatched-pair": true,
    "textlint-rule-common-misspellings": true
  }
}
```

Install the rules as development dependencies in your project:

```bash
npm install --save-dev @textlint-rule/textlint-rule-no-unmatched-pair textlint-rule-common-misspellings
```

### Option 2: Additional Dependencies (Recommended)

You can specify textlint and its rules directly in your pre-commit configuration without requiring NPM dependencies in your project:

```yaml
repos:
  - repo: https://github.com/ryanlewis/pre-commit-mirror-textlint
    rev: v15.1.0
    hooks:
      - id: textlint
        args: ["--rule", "terminology"]
        additional_dependencies:
          - textlint@15.1.0
          - textlint-rule-terminology@5.2.13
```

Create a `.textlintrc` file in your repository root:

```json
{
  "filters": {
    "comments": true
  },
  "rules": {
    "terminology": true
  }
}
```

This approach is particularly useful when you don't want to add NPM dependencies to your project or when working in non-JavaScript projects.

## Version

This repository mirrors textlint version **15.1.0**.

## Links

- [textlint documentation](https://textlint.github.io/)
- [textlint rules collection](https://github.com/textlint/textlint/wiki/Collection-of-textlint-rule)
- [pre-commit framework](https://pre-commit.com/)