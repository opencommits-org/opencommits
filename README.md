# OpenCommits

OpenCommits replaces noisy, inconsistent commit formats with a single clean structure. Plain word order. Instantly readable in any Git interface. Deterministic, automation-friendly, and enforceable with a single canonical regex.

```text
<Type>[!] [scope] description
```

Read the full specification: [opencommits.md](./opencommits.md)

## See the Difference

```
# Conventional Commits
feat(ui): Add accordion menu component
fix: Fix login redirect loop issue
refactor(core): Session cleanup and reorganization
chore(ci): Update pipeline for staging deployments

# OpenCommits
Add ui accordion menu
Fix login redirect loop
Ref core session cleanup
Chr ci update staging pipeline
```

Clean. Consistent. Readable at a glance.

## Quick Start

1. Use one of the Core Types: `Add`, `Fix`, `Ref`, `Opt`, `Rmv`, `Doc`, `Tst`, `Sty`, `Chr`
2. Append `!` for breaking changes: `Fix! api incorrect pagination offset`
3. Optionally add a lowercase scope: `Fix api incorrect pagination offset`
4. Write a concise lowercase description with no trailing period

That's it. No colons. No parentheses. No noise.

## Contributing

OpenCommits is an open standard. Contributions are welcome and encouraged.

- **Found a bug or inconsistency in the spec?** Open an issue.
- **Proposing a change to the standard?** Open a discussion first. Changes to Core Types require maintainer review and an open discussion period before merging.
- **Improving the website?** Visit [opencommits-org/opencommits.org](https://github.com/opencommits-org/opencommits.org).

Read the spec before contributing to understand the design decisions already made.

## License

Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
