# claude-plugins-local

A local-only Claude Code marketplace for plugins under active development on this machine. Never published.

## Layout

- `.claude-plugin/marketplace.json` — marketplace manifest
- `plugins/<name>` — each plugin, typically a symlink to its source repo

## Register & install

From a Claude Code session:

```
/plugin marketplace add ~/projects/claude-plugins-local
/plugin install <plugin-name>@local
```

## Adding a plugin

1. Symlink the plugin's source repo into `plugins/`:
   ```bash
   ln -s /abs/path/to/my-plugin plugins/my-plugin
   ```
2. Append an entry to `marketplace.json` `plugins[]` with `source: "./plugins/my-plugin"`.
3. From a session: `/plugin marketplace update local && /plugin install my-plugin@local`.

## Hot-reload caveat

Claude Code copies the plugin contents into `~/.claude/plugins/cache/local/<plugin>/<version>/` at install time. Edits to the source repo do **not** propagate automatically. After editing:

```
/plugin marketplace update local
/plugin uninstall <plugin>@local
/plugin install <plugin>@local
```

For tighter dev loops, prefer `claude --plugin-dir /abs/path/to/plugin` instead of installing.
