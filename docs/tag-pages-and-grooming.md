# Tag pages and grooming

The registry sets a happy path and enforces nothing. People and agents keep creating tags as they work. Tag pages and grooming are how a vault (or any tagged corpus) catches up with the registry afterwards, with a person reviewing every change to their notes.

## Tag pages
A **tag page** is a note whose front matter `aliases` contains `#<tag>`. Tag Wrangler and similar tools open it when you click the tag. Every registry note is a tag page, so a client that imports registry notes gives those tags their pages.

For a tag that no registry defines (a personal project, a person, an idea), a client may create a **local tag page**:

```yaml
---
tag: project/wifi-router-transition
aliases: ["#project/wifi-router-transition"]
facet: project
status: proposed
replaced_by:
owner: local
---

# project/wifi-router-transition

Definition:
```

Rules for clients:
- Create a page only for a tag with no page anywhere, compared case-insensitively.
- Never stub a tag that any configured registry defines, subscribed or not; the import brings that page. Two notes with the same alias confuse tag tools.
- Keep local pages in their own folder, apart from imported notes, and never stamp them as imported.
- Use the registry note format, so a local page can be proposed upstream by moving it and setting `owner`.
- Leave tags that don't fit `<facet>/<name>` alone; they are grooming candidates.

## Grooming
A grooming pass has five steps. Each produces a proposal the person accepts or rejects; nothing changes in their notes until they accept it.

1. **Inventory.** Tags in use with counts; which have pages; which are registry tags (and their status); which are local.
2. **Normalize.** Propose renames for tags that miss the facet shape or duplicate a registry tag (`#tools/git` → `#tool/git`), and for deprecated tags (→ `replaced_by`).
3. **Pages.** Create missing local tag pages, then draft their `Definition:` lines from how each tag is used.
4. **Backfill.** For each defined tag, propose adding it to notes that match its definition but lack it, with the sentence that justifies each one.
5. **Promote.** Turn local tags a team would share into a pull request here: move the page to `teams/<team>/<facet>/<name>.md`, set `owner`, keep `status: proposed`, run `npm run manifest`.

Mechanical steps (inventory, pages, exact renames) suit a plain client. Steps that need judgment (definitions, backfill, fuzzy renames, choosing what to promote) suit an agent working over the vault and the registry's `definition` lines.

## Never upstream
Named people and organizations, and anything private, stay in the person's own vault or a personal registry. The core holds only generic `with/` kinds; named parties go in a team folder only when that team owns them and they are not private.
