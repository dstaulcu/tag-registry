# Contributing

1. Make a short-lived branch (no long-lived team branches; everything lands on `main`).
2. Add or edit a note under `core/<facet>/` (core group only) or `teams/<team>/<facet>/` following the README naming rules. New tags start as `status: proposed`. A new team (or sub-team, nested inside its parent) needs a `team.md` and a CODEOWNERS line.
3. Run `npm run manifest` and commit the updated `registry.json`.
4. Open a pull request (merge request on GitLab). CI runs `npm run check`. CODEOWNERS routes review to the core group or the team.
5. Accepted tags are set to `active`. Tag a release (`vX.Y`) when the vocabulary changes significantly.

Deprecating: set `status: deprecated` and `replaced_by: <facet>/<name>`. Never delete a note.

Showcase: add an entry to `docs/showcase.md` by pull request, in the format described there.

New facets: open an issue or pull request against `core/facets.md`; the core group decides.

History note: the registry has been restructured in place a few times while it had no other adopters: plural tags became singular (`project/`, `tool/`), then `tactic/` became `technique/` and `community/` was replaced by `area/` and `with/`. Do not rename tags this way again.
