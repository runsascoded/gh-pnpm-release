# gh-pnpm-release

GitHub Action for publishing npm packages with pnpm and creating GitHub releases.

## Quick Start

```yaml
# .github/workflows/release.yml
name: Release
on:
  push:
    tags:
      - 'v[0-9]+.[0-9]+.[0-9]+'
      - 'v[0-9]+.[0-9]+.[0-9]+-*'

jobs:
  release:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      id-token: write
    steps:
      - uses: runsascoded/gh-pnpm-release@v1
        with:
          npm_token: ${{ secrets.NPM_TOKEN }}
```

## How It Works

1. Checks out your code at the tag
2. Sets up pnpm and Node.js, installs dependencies
3. Runs your build command (default: `pnpm run build`)
4. Publishes to npm with `pnpm publish`
5. Creates a GitHub release with auto-generated release notes

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `npm_token` | NPM authentication token | (required) |
| `node_version` | Node.js version | `'20'` |
| `pnpm_version` | pnpm version | `'10'` |
| `build_command` | Build command to run | `'pnpm run build'` |
| `publish_args` | Additional args for `pnpm publish` | `'--access public --no-git-checks'` |

## Usage

Just push a tag:

```bash
git tag v1.0.0
git push origin v1.0.0
```

The action handles building, publishing to npm, and creating the GitHub release with auto-generated notes.

## Used By

- [use-url-params] ([workflow][use-url-params-workflow])
- [og-lambda] ([workflow][og-lambda-workflow])

## See Also

- [gh-pnpm-dist] - Sibling action for building and maintaining npm package distribution branches

[use-url-params]: https://github.com/runsascoded/use-url-params
[use-url-params-workflow]: https://github.com/runsascoded/use-url-params/blob/main/.github/workflows/release.yml
[og-lambda]: https://github.com/runsascoded/og-lambda
[og-lambda-workflow]: https://github.com/runsascoded/og-lambda/blob/main/.github/workflows/release.yml
[gh-pnpm-dist]: https://github.com/runsascoded/gh-pnpm-dist

## License

MIT
