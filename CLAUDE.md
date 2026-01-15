# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Claude Code Plugin Marketplace repository. It serves as a registry for distributing Claude Code plugins that users can install via the marketplace system.

## Repository Structure

```
.claude-plugin/marketplace.json  # Main registry file listing all available plugins
README.md                        # Documentation with installation instructions
```

## Key File: marketplace.json

The `.claude-plugin/marketplace.json` file is the core of this repository. It follows the schema at `https://anthropic.com/claude-code/marketplace.schema.json` and contains:

- **name**: Marketplace identifier
- **description**: Marketplace tagline
- **owner**: Marketplace maintainer info (name, email)
- **plugins**: Array of plugin entries, each with:
  - `name`: Plugin identifier (used in install commands)
  - `description`: What the plugin does
  - `version`: Semantic version
  - `author`: Plugin author info
  - `source`: GitHub source reference (format: `github:owner/repo`)
  - `category`: Plugin category (e.g., "productivity")

## Adding a New Plugin

To add a plugin to this marketplace, add an entry to the `plugins` array in `.claude-plugin/marketplace.json`:

```json
{
  "name": "plugin-name",
  "description": "Plugin description",
  "version": "1.0.0",
  "author": { "name": "author-name" },
  "source": "github:owner/plugin-repo",
  "category": "category-name"
}
```

## Installation Commands

Users install this marketplace with:
```bash
claude /install-marketplace betheproud/lazy-marketplace
```

Then install individual plugins with:
```bash
claude /install <plugin-name>
```
