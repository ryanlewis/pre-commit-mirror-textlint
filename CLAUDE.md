# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a mirror repository for textlint, a pluggable natural language linter for text and markdown. The repository serves as a pre-commit hook distribution point and version tracking system for textlint.

## Repository Structure

- `.version` - Contains the current textlint version being mirrored (currently 15.1.0)
- `.pre-commit-hooks.yaml` - Defines the pre-commit hook configuration for textlint
- `package.json` - Placeholder package file for npm compatibility
- `.npmignore` - Excludes all files from npm publication

## Key Characteristics

- This is a **mirror repository** that tracks textlint versions via git tags and releases
- The primary purpose is to provide pre-commit hook integration for textlint
- Version updates are handled through automated mirroring processes (commits follow "Mirror: X.Y.Z" pattern)
- No source code or development commands are present - this is purely a distribution mechanism
- The pre-commit hook references `textlint@15.1.0` as an additional dependency

## Usage Context

When working with this repository:
- Version updates should maintain the mirroring pattern established in git history
- The `.pre-commit-hooks.yaml` file defines how textlint integrates with pre-commit frameworks
- Changes to `additional_dependencies` version should match the version in `.version`
- This repository does not contain textlint source code or development tooling