# Patchfold

Patchfold is a self-sovereign collaboration layer for git.

Git made code portable. Patchfold makes code collaboration portable: patches,
reviews, provenance, test evidence, and agent work should live with the
repository instead of being trapped inside a single forge.

## Why

Git is already decentralized at the data layer. Every clone can carry the full
history, remotes are interchangeable, and commits can be signed. But modern
collaboration is not decentralized in practice. Pull request conversations,
review approvals, CI evidence, project context, and automation trails usually
belong to GitHub, GitLab, or another hosted forge.

That means the forge becomes the practical source of truth, even when git
remains the technical source of truth.

Patchfold starts from a different premise:

- you own your repository
- you own your identity
- you own your change history
- you own the review and provenance graph around your work
- forges are sync and publishing targets, not the authority

## The Idea

Patchfold treats the patch as the primary unit of collaboration.

A patch is more than a diff. It can carry intent, authorship, review state, test
evidence, signatures, dependencies, comments, and the history of how it changed
over time.

Patchfold should help developers:

- fold messy local work into coherent patches
- unfold a patch to inspect intent, risks, tests, and discussion
- maintain patch stacks without losing context
- sync work to GitHub, GitLab, email, or another remote surface
- preserve collaboration metadata across hosting migrations
- record human and agent contributions as auditable changes

## Non-Goals

Patchfold is not trying to replace git.

Patchfold is not starting as a GitHub replacement.

The first useful version should live alongside existing forges and speak normal
git: commits, branches, remotes, patches, and pull requests should continue to
work.

## First Build Target

Start with a local CLI that can run inside an existing git repository.

The first milestone should be able to:

1. inspect the current repository state
2. group changes into a named patch
3. attach structured metadata to that patch
4. persist Patchfold metadata locally in the repo
5. export the patch as normal git-native artifacts

A tiny, useful command shape might look like this:

```sh
patchfold init
patchfold status
patchfold patch create "explain the change"
patchfold patch show
patchfold export github
```

## Design Principles

- Local-first by default.
- Git-native at the boundaries.
- Portable over platform-specific.
- Signed and auditable where possible.
- Useful before it is complete.
- Forges are integrations, not foundations.
- Agent work should be attributable, reviewable, and reversible.

## Working Tagline

Patchfold makes code collaboration portable.
