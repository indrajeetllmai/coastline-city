# Coastline project instructions

The game is in `outputs/coastline-city` (or the repository root in its standalone checkout).

The user explicitly requested that the game be public on GitHub and that future game changes also be updated on GitHub. After each requested game change, verify the affected behavior, commit the game changes, and publish to `https://github.com/indrajeetllmai/coastline-city` on `main`. No additional publication confirmation is needed within this scope. Preserve unrelated remote changes; never force-push. Do not upload local saves, credentials, unrelated workspace files, or work/ scratch files. If publication fails, report the blocker and do not claim GitHub is current.

The GitHub connector can publish via blobs, a tree, a commit based on the current main commit, and a non-forced ref update if local Git authentication is unavailable. Keep the complete assets/ and vendor/ directories. GitHub Pages should publish main from the repository root.

Keep the local ZIP in sync, excluding .git, .DS_Store, node_modules and Python caches. Use local source and the browser for focused checks.
