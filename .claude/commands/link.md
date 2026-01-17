---
description: Link a plugin from GitHub URL to the marketplace
arguments:
  - name: url
    description: GitHub repository URL (e.g., https://github.com/owner/repo)
    required: true
---

# Link Plugin Command

You are linking a new plugin to the lazy-marketplace.

## Input

GitHub URL: `$ARGUMENTS`

## Task

1. **Parse the GitHub URL** to extract:
   - Owner name
   - Repository name
   - Construct the raw GitHub URL for `.claude-plugin/plugin.json`

2. **Fetch the plugin.json** from the repository:
   - URL pattern: `https://raw.githubusercontent.com/{owner}/{repo}/main/.claude-plugin/plugin.json`
   - If main branch fails, try `master` branch
   - Extract: name, description, version, author, category

3. **Update marketplace.json** at `.claude-plugin/marketplace.json`:
   - Add a new entry to the `plugins` array with:
     ```json
     {
       "name": "<plugin-name>",
       "description": "<plugin-description>",
       "version": "<version>",
       "author": { "name": "<author-name>" },
       "source": {
         "type": "url",
         "url": "https://github.com/{owner}/{repo}.git"
       },
       "category": "<category>"
     }
     ```
   - If plugin with same name exists, update it instead
   - Preserve existing plugins

4. **Update README.md**:
   - Find the "Available Plugins" table
   - Add or update the row for this plugin:
     ```
     | **{name}** | {description} | {version} | {category} |
     ```
   - Keep the table sorted alphabetically by plugin name

5. **Report success** with:
   - Plugin name and version added
   - Confirm both files were updated

## Error Handling

- If URL is invalid, show proper usage: `/link https://github.com/owner/repo`
- If plugin.json not found, inform user the repo needs a `.claude-plugin/plugin.json` file
- If fetch fails, show the error and suggest checking the URL
