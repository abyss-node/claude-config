# Global Claude Code configuration

Everything here is loaded or considered on **every** session, so an entry that
does not earn its attention is a cost paid on all of them. **Add one when a task
has been done badly twice, not in anticipation.** Each entry below names the
failure it exists for.

## Inventory

`CLAUDE.md` — rules true of every project. Anything true of one project belongs
in that project's file instead; a rule with two homes is a defect.

`agents/`

- `consultant` — read-only, `Read`/`Grep`/`Glob` and nothing else. Answers a
  cross-lane question in its own window so the caller does not spend theirs on
  the other stack. The tool list is what makes the lane boundary real rather
  than advisory: a session can learn anything about the other side and change
  nothing. Exists because reading Rust from a TypeScript session, or Django from
  a React one, has repeatedly eaten a window that was needed elsewhere.
  Deliberately one agent, not one per stack: a global consultant cannot name a
  repo's actual contract artefact, and two that name nothing are one listed
  twice. A repo adds its own named consultant when it has a path worth
  hardcoding — see `/lanes`.
- `code-reviewer` — reviews a diff against *this* project's failure modes, having
  first read the project's own stated invariants. Explicitly forbidden from style
  commentary and from manufacturing findings. Exists as a delegatable
  independent voice: per `CLAUDE.md`, verification never goes to the agent that
  did the work.

`commands/`

- `checkpoint` — verify, report what was *not* run, confirm no scratch or secret
  is staged, propose a commit, stop. The frequent lightweight one; `/ship` and
  `/land-and-deploy` are the heavy release path.
- `lanes` — sets a repo up with lane boundaries, role commands and nested
  `CLAUDE.md` files. Run once per multi-stack repo.

`settings.json` — model, hooks (gbrain sync), plugins, permissions. Not
tracked: it names a private project in its hooks and a client host in its
permissions. `settings.template.json` is the redacted form, and is what a new
machine copies from.

## Known overlaps, left deliberately

These duplicate each other and the duplication is not yet resolved. Recorded so
the next decision is made on evidence rather than rediscovered:

- **Review**: the built-in `/code-review`, gstack's `/review`, and the
  `code-reviewer` agent. The agent is the one that reads project invariants first
  and the one that can be delegated inside a workflow; the skills are the
  interactive paths.
- **Debugging**: gstack's `/investigate` versus the Debugging section of
  `CLAUDE.md`. The section is the always-on rule; the skill is the driven
  procedure. If `/investigate` starts contradicting it, the section wins and the
  skill should be edited.
- **Planning**: gstack's `/spec` versus the Task classification section. Same
  split — rule always on, skill driven.
- **Writing voice**: resolved 2026-08-25. The three anti-slop skills
  (`tropes-fyi-writing`, `anti-ai-slop-writing`, `no-ai-slop`) were deleted —
  they answered to the same phrasing as each other, and the 2026-07-31 detector
  study found surface-tell editing does not survive a provenance-tracking
  detector anyway. `personal-voice` is the survivor and carries the discipline
  inline. Backup at `backups/skills-removed-2026-08-25/`.

## Skills

Halved on 2026-09-15, from 121 to 59. The larger vendor pack went once the
single project it served closed — 61 entries charged to every session's listing
budget for work that had finished — and one personal skill followed, its source
already living in its own repo. What is left is still mostly one pack serving
one project, so the same argument comes round again. Two rules apply meanwhile:

**Name a skill exactly when a `CLAUDE.md` points at one.** A category matches
several, and the wrong one will be picked.

**Prefer a house rule written against the actual repo over a generic advisory
pack.** A general-purpose reviewer knows nothing about a given codebase's failure
modes. Where a pack is worth something, rebuild the part that is rather than
installing the whole thing.
