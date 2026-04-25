# claude-plugins

Personal Claude Code plugin marketplace. Index of my plugins; each plugin lives in its own GitHub repo.

## Register & install

From a Claude Code session:

```
/plugin marketplace add heiyan-2020/claude-plugins
/plugin install <plugin-name>@claude-plugins
```

(Or with the full URL `git@github.com:heiyan-2020/claude-plugins.git` / `https://github.com/heiyan-2020/claude-plugins.git`.)

## Currently registered

- **vibe-slides** — author academic slide decks via a markdown DSL → pptxgenjs. Source: [heiyan-2020/vibe-slides](https://github.com/heiyan-2020/vibe-slides).

## Adding a plugin

1. Push the plugin to its own GitHub repo (must contain `.claude-plugin/plugin.json`).
2. Append to `.claude-plugin/marketplace.json` `plugins[]`:

   ```json
   {
     "name": "my-plugin",
     "source": { "source": "github", "repo": "heiyan-2020/my-plugin" },
     "description": "...",
     "category": "...",
     "version": "x.y.z"
   }
   ```

3. Commit + push this marketplace repo. Then on any machine:
   `/plugin marketplace update claude-plugins && /plugin install my-plugin@claude-plugins`.

## Iterating

Claude Code **copies** plugin contents into `~/.claude/plugins/cache/claude-plugins/<plugin>/<version>/` at install time, not symlink/live-read. After editing a plugin and pushing:

```
/plugin marketplace update claude-plugins
/plugin uninstall <plugin>@claude-plugins
/plugin install <plugin>@claude-plugins
```

For tight dev loops, skip the marketplace and run claude directly against the plugin source:

```bash
claude --plugin-dir ~/projects/<plugin>
```

`--plugin-dir` reads live from disk and reloads on `/reload-plugins`.

## Pinning versions

To pin a plugin to a specific git ref instead of `main`, add a `ref` field to its source:

```json
"source": { "source": "github", "repo": "heiyan-2020/vibe-slides", "ref": "v0.1.0" }
```
