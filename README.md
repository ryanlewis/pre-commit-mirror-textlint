# textlint pre-commit hook

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