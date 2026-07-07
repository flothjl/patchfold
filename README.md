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

## Proof in the Wild

Some of the most important software in the world already collaborates through
patches instead of platform-native pull requests.

The [Linux kernel](https://docs.kernel.org/process/submitting-patches.html),
[Git itself](https://git-scm.com/docs/SubmittingPatches),
[PostgreSQL](https://wiki.postgresql.org/wiki/Submitting_a_Patch),
[QEMU](https://www.qemu.org/docs/master/devel/submitting-a-patch.html),
[Xen](https://wiki.xenproject.org/wiki/Submitting_Xen_Project_Patches), and
many other projects use email-centered patch workflows because patches are
portable, inspectable, replyable, archivable, and independent of any single code
forge. A patch can move through mailing lists, local clones, maintainer trees,
release branches, and long-lived public archives without needing GitHub or
GitLab to be the system of record.

That model has real strengths:

- the patch is the unit of review
- the discussion can outlive any hosting platform
- maintainers can apply, amend, queue, and forward work with plain git tools
- contributors can participate without joining one company's collaboration silo
- project history stays closer to the repository than to a web app

But the experience is clunky for most modern teams.

Email patch workflows ask contributors to understand mailing list etiquette,
`git format-patch`, `git send-email`, versioned patch series, reviewer-specific
CC lists, archive links, threading, local application with `git am`, and the
social norms of each project. The result is powerful and sovereign, but hard to
enter, hard to automate, and hard to connect to the review expectations teams
learned from pull requests.

Patchfold is an attempt to keep the sovereignty of patches while giving them a
modern collaboration surface.

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

## What Needs to Exist

For collaboration to be portable, the patch cannot be the only portable object.
The surrounding workflow has to move too.

Patchfold needs a small set of git-adjacent collaboration objects:

- patch intent and summary
- patch stack dependencies
- review comments and requested changes
- approvals and maintainer decisions
- test results and build evidence
- identity and signature metadata
- agent actions and generated work logs

Those objects should be:

- stored locally enough to survive offline work
- exportable as normal git artifacts when needed
- syncable through more than one network path
- readable without one company's web UI
- attributable to stable identities instead of platform accounts alone
- private or encrypted when the collaboration context requires it

This is where modern self-sovereign infrastructure helps. DID-addressed
identity, protocol-scoped records, encrypted data, subscriptions, and
live/durable sync give Patchfold a way to model collaboration as portable data
rather than platform state. A system like [Enbox](https://github.com/enboxorg/enbox)
could be one transport and storage layer for that: not the center of Patchfold's
identity, but a useful substrate for moving patch metadata, reviews, and
provenance between collaborators who should control their own endpoints.

The important part is the boundary: Patchfold should define the git-native
collaboration model. Transports such as DWNs, email, forges, or future relays
should move that model without owning it.

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
