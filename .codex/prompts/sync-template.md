Sync the `.codex/` directory from the upstream orchestrated-project-template repository into this project.

## Recommended flow

1. Clone the upstream repository into a temporary directory.
2. Copy the upstream `.codex/` subtree into this project.
3. Review the diff before committing.
4. Keep project-specific changes outside `.codex/templates/` when possible so future syncs stay reviewable.

## Example shell flow

```bash
SYNC_TMP=$(mktemp -d /tmp/template-sync-XXXXXX)
git clone --filter=blob:none --sparse https://github.com/josipjelic/orchestrated-project-template "$SYNC_TMP"
cd "$SYNC_TMP" && git sparse-checkout set .codex
rsync -av --delete "$SYNC_TMP/.codex/" ./.codex/
rm -rf "$SYNC_TMP"
```

If you are on Windows without `rsync`, use PowerShell `Copy-Item` / `Remove-Item` equivalents and review the resulting git diff carefully.
