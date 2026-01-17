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
   - First, check if a plugin with the same `name` already exists in the `plugins` array
   - **If plugin exists**: Update all fields (description, version, author, source, category) with the new values from plugin.json
   - **If plugin is new**: Add a new entry to the `plugins` array
   - Plugin entry format:
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
   - Preserve all other existing plugins unchanged

4. **Update README.md**:
   - Find the "Available Plugins" section
   - **If plugin exists**: Find and update the existing plugin card with new information
   - **If plugin is new**: Add a new plugin card
   - Card format (each plugin should follow this exact format):
     ```markdown
     ---

     ### [{name}](https://github.com/{owner}/{repo})

     {description}

     `v{version}` · `{category}`

     ```bash
     /plugin install {name}
     ```

     ---
     ```
   - The plugin name in the heading should be a clickable link to the GitHub repository
   - The install command should be in a bash code block for easy copying with GitHub's copy button
   - Keep plugins sorted alphabetically by name

5. **Report success** with:
   - Indicate whether plugin was **added** (new) or **updated** (existing)
   - Show plugin name and version
   - Confirm both files were updated

## Error Handling

- If URL is invalid, show proper usage: `/link https://github.com/owner/repo`
- If plugin.json not found, inform user the repo needs a `.claude-plugin/plugin.json` file
- If fetch fails, show the error and suggest checking the URL
