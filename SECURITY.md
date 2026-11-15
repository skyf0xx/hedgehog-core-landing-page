# Security Policy

## Reporting a vulnerability

Report privately through GitHub's advisory form:

**https://github.com/skyf0xx/hedgehog-core-landing-page/security/advisories/new**

That channel is private between you and the maintainers, and it lets a
fix land before the details are public.

If the form is unavailable, open a normal issue with only the affected
component and the words "security — details on request", and a private
channel will be arranged from there. Don't put the reproduction in a
public issue in that case.

Expect an acknowledgement within a few days. You'll get the assessment,
the fix if there is one, and credit in the release notes unless you'd
rather not be named.

## Supported versions

Fixes land on the latest released version. There are no long-term
support branches.

## What's in scope

This package is Hedgehog's landing-page core: agents, skills, and a
pre-built Astro workspace (`workspace/`) that a consuming project
installs and builds. The interesting boundaries:

- **The installed payload** (`agents/`, `skills/`, `CLAUDE.core.md`) —
  these files are copied verbatim into every consuming project, so a
  change that makes a build agent take instructions from untrusted
  content, or that weakens a gate a project relies on, is a
  supply-chain issue.
- **The workspace template** (`workspace/`) — a dependency pin, script,
  or config that runs attacker-controlled code at install or build time,
  or ships a lockfile that does not match `package.json`.
- **Prompt injection reaching the build agents** through content they
  read — a brief, BMAD planning output, source material for copy, a
  design handoff file. Reports here are welcome and are treated as real,
  not theoretical.

## What's out of scope

- Vulnerabilities in dependencies with no Hedgehog-specific exploit
  path — report those upstream.
- Anything that requires the attacker to already control the machine
  running the build, or to have write access to the repository.
- Visual or copy quality defects in a generated page — those are
  quality bugs, not security issues. Open a normal issue instead.

## A note on local-only impact

Most of this core's attack surface is local: the inputs are a
project's own brief and chain files. That lowers severity but doesn't
put a report out of scope. In this tool's model those files are
frequently written by AI agents rather than by a person, so "the input
comes from the project itself" is not the same assurance it would be
in a hand-written codebase — an agent that has been misled is a
plausible source of hostile input.
