# Building a client

A client reads a registry and puts its tags somewhere useful: an Obsidian vault, an editor, a CLI, a linter, an agent's prompt. Read the [specification](specification.md) first; this page is the practical advice.

## Fetching
1. Get `registry.json` from the repository root. Anonymous raw HTTPS works for public repos. A local `git` shallow clone or a read-only token over the host's API works for private ones.
2. Refuse a manifest whose `version` you do not know.
3. Fetch only what the user subscribed to: core, plus chosen teams (and, by default, their ancestors via `parent`).

## Validating
- Verify each downloaded note against `tags[].hash` before using it. If any hash fails, abort the whole run rather than applying part of it.
- Reject unsafe paths (absolute paths, `..`, hidden folders) in `path` and in any destination setting.
- Read `facet` and `source` from the manifest, never from `path`.
- Ignore manifest fields you do not recognise.

## Writing
- Preview, then apply. Show new, updated, unchanged and conflicting notes before touching anything.
- Record where each note came from (a stamp such as the note's hash in front matter, with a key name of your choosing). Compare it with the current upstream hash to tell a local edit from an upstream change.
- Never silently overwrite a local edit. Default to keeping the user's version and offer "use theirs" and "save theirs as a copy".
- Never delete a note because a tag or team disappeared upstream. Report it.
- Treat `status: deprecated` as a prompt, not an action: show the `replaced_by` tag, and make rewriting existing notes opt-in.
- Hide teams with `example: true` unless the user asks.

## Privacy
Contact only the hosts the user configured. Do not ship a default registry. Keep tokens out of logs, notices and diagnostics, and store them in the platform's secret storage when it exists.

## Multiple registries
Let users add several (for example public plus internal). On a duplicate tag, the earlier registry wins; make the order visible and editable.

## Reference implementation
[Tag Registry Sync](https://github.com/dstaulcu/obsidian-tag-registry) is an Obsidian plugin that implements the behaviour above: three access methods, team picker, preview/apply, conflict handling, optional startup check. Its source is the best worked example of these rules.

## Ideas for other clients
See [ideas](ideas.md).
