# OpenCommits
**Commit Message Standard**

OpenCommits is a minimal commit message standard for software teams. It replaces inconsistent formats with a single clean structure that is readable in any Git interface.

## At a Glance

```
Type[!] [scope] description
```

| Part | Required | Example |
|---|---|---|
| `Type` | Yes | `Fix` |
| `!` | Only for breaking changes | `Fix!` |
| `scope` | No | `api` |
| `description` | Yes | `incorrect pagination offset` |

```
Fix! api incorrect pagination offset
```

## Why OpenCommits

**Common format:**
```
feat(ui): Add accordion menu component
fix: Fix login redirect loop issue
refactor(core): Session cleanup and reorganization
chore(ci): Update pipeline for staging deployments
fix(a11y): Fix missing aria labels on modal
perf(db): optimize transaction batching
```

**OpenCommits:**
```
Add ui accordion menu
Fix login redirect loop
Ref core session cleanup
Chr ci update staging pipeline
Fix a11y missing aria labels on modal
Opt db transaction batching
```

OpenCommits is easier to scan, consistent in rhythm, and free of colons, parentheses, and noisy punctuation.
It preserves natural sentence flow while enforcing a strict 3-character Type prefix.
That makes commit history readable by humans, not just parsers.

## Format

```
Type[!] [scope] description
```

- **Type** — a 3-letter capitalized identifier describing the intent of the change
- **!** — optional modifier appended directly to the Type, signals a breaking change
- **scope** — optional lowercase domain identifier
- **description** — lowercase, concise, human-readable, no trailing period

No colons. No parentheses. No brackets. No mandatory footers.

## Compliance Profiles

OpenCommits defines two compliance profiles so teams and tooling can be explicit:

- **Core profile** — only Core Types are valid
- **Extended profile** — Core + Extended Types are valid

Core profile regex:

```
^(Add|Fix|Ref|Opt|Rmv|Doc|Tst|Sty|Chr|Rev)(!)?( [a-z][a-z0-9]*){0,2} [a-z].+$
```

Extended profile regex:

```
^(Add|Fix|Ref|Opt|Rmv|Doc|Tst|Sty|Chr|Mov|Rnm|Dep|Sec|Cfg|Rev)(!)?( [a-z][a-z0-9]*){0,2} [a-z].+$
```

## Types

Types are divided into a **Core set** and an **Extended set**.

The Core set covers the vast majority of commits and is enough for most teams. The Extended set is officially defined for teams that benefit from extra precision. When used consistently, they mean the same thing everywhere.

### Core Types

Core Types are mandatory for OpenCommits compliance.

#### `Add`
**New features or capabilities.**
```
Add ui accordion menu
Add api token refresh endpoint
Add auth session timeout setting
```

#### `Fix`
**Bug fixes or incorrect behavior.**
```
Fix login redirect loop
Fix a11y missing aria labels on modal
Fix api pagination off by one
```

#### `Ref`
**Internal refactoring and cleanup.**
Structural changes that do not alter external behavior, such as reorganizing code, extracting methods, or simplifying logic.
```
Ref core session cleanup
Ref ui header rendering logic
Ref api error handling
```

#### `Opt`
**Performance optimizations.**
Use when the primary goal is speed, efficiency, or resource reduction.
```
Opt db index on transactions
Opt api response batching
Opt cache eviction strategy
```

#### `Rmv`
**Removal of code, features, or files.**
Dead code, obsolete functionality, deprecated APIs that have been fully removed.
```
Rmv v1 auth endpoints
Rmv unused cache layer
Rmv legacy feature flags
```

#### `Doc`
**Documentation and comments.**
README, API docs, architecture docs, inline comments.
```
Doc auth token lifecycle
Doc local setup instructions
Doc api rate limit behavior
```

#### `Tst`
**Tests and test-related changes.**
Any test-only change: adding, updating, or fixing tests.
```
Tst add jwt expiration edge cases
Tst update e2e checkout flow
Tst fix flaky session test
```

#### `Sty`
**Style and formatting.**
Purely cosmetic changes: formatting, linting, prettier. No logic changes.
```
Sty format backend files
Sty apply prettier to ui
Sty fix lint warnings
```

#### `Chr`
**Maintenance and tooling changes.**
Tooling, CI/CD, dependency updates, build scripts, infrastructure, dev configuration.
```
Chr update ci pipeline
Chr bump node to 22
Chr upgrade react to 19
Chr update eslint config
```

#### `Rev`
**Commit reversals.**
Revert of a previous commit while preserving history.
```
Rev fix api timeout
Rev add new checkout flow
Rev ref core cache manager
```

Do not repeat “revert” in the description — `Rev` already communicates intent. Reference the original commit's Type and description to keep the history traceable. In the commit body, include the reverted commit hash when available.

`Rev!` is valid when the rollback itself introduces a breaking change.

### Extended Types

Extended Types are optional. Teams adopt them when the distinction adds meaningful value to their history. Because they are officially defined in this spec, they mean the same thing in every codebase that uses them.

#### `Mov`
**File or module moves.**
```
Mov ui components to shared/ui
Mov core helpers to common/utils
```

#### `Rnm`
**Identifier, file, or module renames.**
```
Rnm user_service to account_service
Rnm loginError to authError
```

#### `Dep`
**Deprecation of features or APIs.**
Mark functionality as deprecated but not yet removed. Pairs naturally with a future `Rmv`.
```
Dep v1 user endpoints
Dep legacy session tokens
```

#### `Sec`
**Security-specific changes.**
Use when security-related work requires explicit visibility or audit traceability.
```
Sec fix csrf vulnerability in forms
Sec patch xss vector in comment renderer
```

#### `Cfg`
**Configuration-only changes.**
```
Cfg update app manifest
Cfg adjust webpack production settings
Cfg update editorconfig rules
```

## Type Selection Rules

When multiple Types seem plausible, use these tie-break rules:

- `Add` over `Ref` when user-facing capability is added
- `Fix` over `Ref` when incorrect behavior is corrected
- `Opt` only when performance improvement is the primary intent
- `Cfg` for configuration-only diffs (runtime, tooling, project config files)
- `Chr` for maintenance/tooling/dependency/CI work that is not config-only
- `Ref` for structural code changes with no behavior change
- `Mov`/`Rnm` when move/rename intent should stay visible in history
- `Sec` when security visibility or audit traceability is a primary goal

## Breaking Changes

Append `!` directly after the Type to signal a breaking change. This works with any Type.

```
Rmv! v1 auth endpoints
Add! new response schema for orders
Fix! price rounding now uses banker's rounding
Ref! core session model
```

`!` means consumers need to take action. Document the impact in the commit body when possible.

## Scopes

Scopes are optional lowercase identifiers that describe where in the system the change occurred. Use them when they add context. Omit them when the description is already clear.
Scope terms should be stable domain nouns (for example `api`, `ui`, `auth`, `ci`, `spec`), not action words.

**Common scopes:**
```
ui, api, db, core, auth, a11y, loc, cache, ci, inf, web, mobile, admin, shared
```

**With scope:**
```
Fix a11y focus trap on modal
Add ui drag and drop support
Opt db transaction batching
Chr ci update deploy pipeline
```

**Without scope:**
```
Fix login redirect loop
Add dark mode toggle
Doc deployment guide
```

Prefer a single scope. Use two only when both are genuinely necessary:
```
Fix ui a11y button contrast
Ref core api request builder
```

Scope decision rule:

- Default to no scope
- Add one scope only when omitting it would hide meaningful location context
- Use two scopes only for true cross-boundary changes
- If uncertain, prefer no scope over speculative scope
- Scope should be a domain noun, not a verb/adjective (`improve`, `update`, `better` are invalid scope terms)

## Descriptions

Descriptions should be lowercase, concise, specific, and have no trailing period.
Prefer natural sentence flow whenever possible to reduce scan effort in `git log --oneline`.

**Good:**
```
Fix a11y missing aria labels on modal
Add ui accordion menu with keyboard navigation
Opt db index on high-traffic transactions table
Doc auth token lifecycle and refresh flow
```

**Bad:**
```
Fix issue
Add stuff
Ref code
Update things
```

Write for someone scanning `git log --oneline` at speed.

Common corrections (invalid or too vague -> stronger):

```
fix login redirect loop                     -> Fix login redirect loop
Fix API pagination issue                    -> Fix api pagination issue
Fix login redirect loop.                    -> Fix login redirect loop
Add ui                                      -> Add ui profile menu
Chr update stuff                            -> Chr ci update deploy workflow
Ref ui api                                  -> Ref ui api request builder
Rev revert fix login redirect loop          -> Rev fix login redirect loop
Sec fix csrf vulnerability in forms.        -> Sec fix csrf vulnerability in forms
Cfg Update webpack production settings      -> Cfg update webpack production settings
Fix! api breaking pagination changes        -> (too vague) -> Fix! api pagination now returns zero-indexed results
```

## SemVer Mapping

| Type | SemVer Impact |
|---|---|
| Any type with `!` | MAJOR |
| `Add` | MINOR |
| `Dep` | MINOR (signals future MAJOR) |
| `Fix`, `Sec` | PATCH |
| `Ref`, `Opt`, `Rmv`, `Mov`, `Rnm` | Internal — no bump |
| `Doc`, `Tst`, `Sty`, `Chr`, `Cfg`, `Rev` | No version bump |

Any Type suffixed with `!` maps to MAJOR regardless of its default.

## Example History

```
Add ui accordion menu with keyboard support
Fix a11y focus trap on settings modal
Fix! api pagination now returns zero-indexed results
Ref core session cleanup
Opt db transaction batching for order writes
Tst add edge cases for jwt expiration
Chr ci update staging deploy pipeline
Chr bump node to 22
Doc auth token lifecycle and refresh flow
Sty apply prettier across backend
Dep v1 user endpoints
Rmv! v1 auth endpoints
Rev add experimental sidebar
```

## Best Practices

- Keep commits small and focused on a single intent — one Type per commit
- Use a scope when it genuinely clarifies where the change is; omit it when the description is self-sufficient
- Use `Dep` before `Rmv` for public-facing APIs to give consumers a migration window
- Use `!` sparingly — describe the impact in the commit body when you do
- Use `Rev` instead of rewriting history
- Prefer dedicated commits for refactor, move, rename, and optimize — mixing them with feature work hides intent

## Migration from Conventional Commits

| Conventional Commits | OpenCommits |
|---|---|
| `feat` | `Add` |
| `fix` | `Fix` |
| `refactor` | `Ref` |
| `perf` | `Opt` |
| `docs` | `Doc` |
| `test` | `Tst` |
| `style` | `Sty` |
| `chore` | `Chr` |
| `revert` | `Rev` |
| `BREAKING CHANGE` / `!` | `!` suffix |

## FAQ

**Are scopes required?**
No. Use them only when they add clarity.

**Do types have to be capitalized?**
Yes. 3-letter capitalized Type, lowercase everything else. This creates a consistent visual rhythm in git history.

**Should I use core or extended types?**
Start with core. Add extended types if your team finds the distinction useful — large teams working across many modules often benefit from `Mov` and `Rnm` being separate from `Ref`.

**Can I add custom types?**
Strongly discouraged. Custom types fragment the ecosystem and break tooling. If you feel a gap exists, open an issue at https://github.com/opencommits-org/opencommits.

**Is this compatible with Conventional Commits tooling?**
With a simple type mapping (see Migration section), yes. The mapping is mechanical.

**How strict is this standard?**
Strict on type semantics. Flexible on scope usage. Forgiving on description tone as long as it is clear and specific.

## Appendix: Complete Type Reference

| Type | Set | SemVer | Description |
|---|---|---|---|
| `Add` | Core | MINOR | New features or capabilities |
| `Fix` | Core | PATCH | Bug fixes or incorrect behavior |
| `Ref` | Core | — | Internal refactoring and cleanup |
| `Opt` | Core | — | Performance optimizations |
| `Rmv` | Core | — | Removal of code, features, or files |
| `Doc` | Core | — | Documentation and comments |
| `Tst` | Core | — | Tests and test-related changes |
| `Sty` | Core | — | Style and formatting |
| `Chr` | Core | — | Maintenance and tooling changes |
| `Rev` | Core | — | Commit reversals |
| `Mov` | Extended | — | File or module moves |
| `Rnm` | Extended | — | Identifier, file, or module renames |
| `Dep` | Extended | MINOR | Deprecation of features or APIs |
| `Sec` | Extended | PATCH | Security-specific changes |
| `Cfg` | Extended | — | Configuration-only changes |

## Appendix: Validation Pattern

Extended profile normative validation pattern:

```
^(Add|Fix|Ref|Opt|Rmv|Doc|Tst|Sty|Chr|Mov|Rnm|Dep|Sec|Cfg|Rev)(!)?( [a-z][a-z0-9]*){0,2} [a-z].+$
```

This validates a valid Type, an optional `!`, zero to two lowercase scope tokens, and a lowercase description.
Regex alone does not semantically decide scope vs description when scope is omitted. For deterministic tooling, apply the scope allowlist parser rule below.

Deterministic parsing rule for tooling:

- Projects should define a scope allowlist
- Token 2 is treated as scope only when it matches the allowlist (or two allowlisted tokens)
- If token 2 is not allowlisted, parse from token 2 as description start

Core profile validation pattern:

```
^(Add|Fix|Ref|Opt|Rmv|Doc|Tst|Sty|Chr|Rev)(!)?( [a-z][a-z0-9]*){0,2} [a-z].+$
```

Strict profile — single scope only:

```
^(Add|Fix|Ref|Opt|Rmv|Doc|Tst|Sty|Chr|Mov|Rnm|Dep|Sec|Cfg|Rev)(!)?( [a-z][a-z0-9]*)? [a-z].+$
```

*OpenCommits — Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)*
