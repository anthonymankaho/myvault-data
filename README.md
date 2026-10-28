# MyVault OS data

This public repository contains the data displayed by [MyVault OS](https://anthonymankaho.github.io/myvault-os/).

- `vault.json`: 43 skills, 38 projects, and 3 documents, with full Markdown note bodies, tags, links, and source references.
- `second-brain/`: complete copies of 82 Markdown files and 2 Obsidian canvases, plus the source `.gitignore`.
- Canvas records retain their complete nodes, positions, text, and connections in the `canvas` field.

Git history and Obsidian application settings are excluded from the source mirror. Existing record IDs, project statuses, and unrelated vault data are preserved during import.

To refresh the import, use `tools/import-obsidian.mjs` from the website repository with the source folder and this checkout's path. Review and commit the changes before pushing.
