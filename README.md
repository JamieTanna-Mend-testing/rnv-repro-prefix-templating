# rnv-repro-prefix-templating

Minimal reproduction of `commitMessagePrefix` not being templated in config file commits (Config Migration and onboarding).

`renovate.json` sets a templated `commitMessagePrefix`, and uses `"dependencyDashboard": true`, which Renovate's config migration rewrites to `{ "enabled": true }`.

## Expected

The Config Migration PR title and commit message are:

```
WSD-0000 | chore(config): migrate Renovate config
```

## Actual (before the fix)

The raw template is used:

```
WSD-0000 | {{semanticCommitType}}{{#if semanticCommitScope}}({{semanticCommitScope}}){{/if}}: migrate Renovate config
```

## Onboarding

Onboarding shares the same code path, but the repository has no config at that point, so the prefix would need to come from global/inherited config (e.g. `RENOVATE_COMMIT_MESSAGE_PREFIX`) on a repository without a `renovate.json`. This isn't covered by this repository.
