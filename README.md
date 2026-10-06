# bun-lockfile-v2-dependabot-repro

Repro repository for [dependabot/dependabot-core#16026](https://github.com/dependabot/dependabot-core/issues/16026).

Bun 1.4 introduced a new `bun.lock` text lockfile with `lockfileVersion: 2`. Dependabot's bundled Bun binary only supports up to lockfileVersion 1, so Dependabot updates fail with:

```
Unsupported bun.lock 'lockfileVersion' 2 in /bun.lock. The bun version Dependabot runs supports up to 1.
```

## Contents

- `package.json` - minimal Bun project with one dependency (`is-odd`).
- `bun.lock` - lockfile in the new v2 text format (as produced by Bun 1.4+).
- `.github/dependabot.yml` - Dependabot configuration enabling the `bun` ecosystem, plus `docker` and `github-actions` ecosystems.

## Expected behavior

Dependabot should be able to parse `bun.lock` and open update PRs for the `bun` ecosystem.

## Actual behavior

Dependabot update runs fail because the bundled Bun version cannot parse `lockfileVersion: 2`.
