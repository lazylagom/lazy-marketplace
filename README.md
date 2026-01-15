# Lazy Marketplace

> Stay Lazy, Act Crazy

A curated Claude Code plugin marketplace for developers who want to work smarter, not harder.

## Quick Start

### 1. Add the Marketplace

```bash
claude /install-marketplace betheproud/lazy-marketplace
```

### 2. Install a Plugin

```bash
claude /install <plugin-name>
```

## Available Plugins

| Plugin | Description | Version | Category |
|--------|-------------|---------|----------|
| **imlazy** | A cognitive mode-based agent system that thinks like a developer | 0.1.0 | productivity |

### imlazy

A smart agent workflow system that adapts to your cognitive load. It provides different operational modes (lazy-low, lazy-medium, lazy-high) to match how developers actually think and work.

**Install:**
```bash
claude /install imlazy
```

**Source:** [github:lazylagom/lazy-marketplace](https://github.com/lazylagom/lazy-marketplace)

## Contributing

Want to add your plugin to the marketplace? Submit a PR with your plugin entry in `.claude-plugin/marketplace.json`:

```json
{
  "name": "your-plugin",
  "description": "What your plugin does",
  "version": "1.0.0",
  "author": { "name": "your-name" },
  "source": "github:owner/repo",
  "category": "category"
}
```

## License

MIT
