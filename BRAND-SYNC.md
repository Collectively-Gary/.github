# Shared Gary brand source

The authoritative, versioned brand kit is `Collectively-Gary/GaryOS/brand`.
`BRAND-SOURCE.json` records the source commit, brand tree, and SHA-256 of every
vendored file. The existing brand copies are identical at adoption. Downloads
are asset intake, not the distribution source; raw iPhone footage remains off Git.

Propose asset changes in the source repository first. After merging them, fetch
its default branch and use the private `samtuckerdavis/workspace-sync` tooling:

```sh
python3 brand_sync.py --source ~/Desktop/Collectively-Gary/GaryOS --target /path/to/consumer
# Review drift, create an isolated branch/worktree, then write the update:
python3 brand_sync.py --source ~/Desktop/Collectively-Gary/GaryOS --target /path/to/consumer --apply
```

The command copies committed source blobs and updates the lock. It refuses dirty
checkouts, default branches, symlinks, and archived repositories; extra tracked
brand files need manual review. It never deletes assets, commits, or pushes.
Review and commit the resulting diff through a PR in each active consumer.
Archived copies remain frozen, and the GaryOS app submodule pin is updated in a
separate explicit PR. No scheduled updates or automatic merges are enabled.

For the canonical source itself, change brand files through a source PR, then
regenerate its provenance lock from the committed source tree. Its source_commit
can precede a provenance-only commit because source_tree pins the exact assets.
