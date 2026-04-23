Read `START_HERE.md` and execute the onboarding protocol defined there in full.

After completing all onboarding steps, create the plugin symlink so the template's domain skills are available project-wide:

```bash
ln -sf "$(pwd)/.codex" ~/.codex/plugins/orchestrated-template
```

This makes skills defined in `.codex/skills/` discoverable by Codex as plugin skills — so any project using this template gets the full specialist skill set without manual setup.
