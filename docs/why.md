# Why a shared tag registry

## The problem
Tags drift. One vault says `#tool/github`, another `#tools/gh`, a third `#git-hub`. A team of ten people ends up with ten vocabularies, so nothing can be rolled up, searched across vaults, or handed to an agent with confidence. Meaning drifts too: nobody remembers whether `#project/data-lake` was a project or a tool.

## What the registry does
It is one repository that is the source of truth for the vocabulary. Every tag is a small note with a definition, a status and an owner. Clients (such as the [Tag Registry Sync](https://github.com/dstaulcu/obsidian-tag-registry) Obsidian plugin) copy the tags you subscribe to into your vault, so your tag pane, autocomplete and agents all see the same names and the same definitions.

## Six facets as a query model
Every tag is `<facet>/<name>`. Each facet answers a different question, so a single note can carry several and you can slice work along any of them.

| Facet | Question it answers |
| --- | --- |
| `area` | Which part of life is this? (home, work, health, fitness, finance, learning) |
| `with` | Who does it involve? |
| `objective` | Which goal does it serve? |
| `project` | Which bounded effort is it part of? |
| `technique` | Which capability or method did it use? |
| `tool` | Which service, software or system was involved? |

A work log bullet such as `#area/work #objective/faster-onboarding #project/new-hire-kit #technique/agent-scheduling #tool/github` can be rolled up by goal for a leader, by project for the team, or by technique for a community of practice, without anyone retagging.

## Home and work
The core is deliberately generic: `area` covers home and work, `with` covers family and customers, and nothing in core names a person or an organization. Personal use needs no team at all; an organization adds a team folder for its own projects, objectives and systems.

## Core and teams
- **Core** is small, slow-moving and reviewed by a core group.
- **Teams** own their own values under `teams/<team>/` and can nest as deeply as the organization does. Tag names are unique across all of it, and a team tag that several teams use can be promoted into core.

## What it is not
- It does not scan or rewrite your vault. Clients import notes; renaming tags in existing notes is the client's optional, opt-in feature.
- It does not enforce usage. It makes the right tag easy to find and the meaning unambiguous.
- It is not tied to Obsidian. The format is markdown plus a JSON manifest, so any tool that reads tags can use it.

Next: the [specification](specification.md), then [building clients](building-clients.md).
