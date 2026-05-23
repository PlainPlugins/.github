# PlainPlugins `.github`

Org-wide policy, conventions, reusable CI workflows, and community-health files for the [Plain Plugins](https://github.com/PlainPlugins) GitHub organization.

## What lives here

- **[`CONVENTIONS.md`](./CONVENTIONS.md)**: the canonical naming convention for every Plain Plugins repo. Single source of truth for blocks, hooks, options, CPT keys, slugs, namespaces, and constants.
- **[`profile/README.md`](./profile/README.md)**: rendered on the org homepage at <https://github.com/PlainPlugins>.
- **[`.github/workflows/`](./.github/workflows/)**: reusable GitHub Actions workflows. Every plugin's CI references these via `uses: PlainPlugins/.github/.github/workflows/<file>.yml@main`. Stops CI YAML from being copy-pasted across repos.
- **[`.github/PULL_REQUEST_TEMPLATE.md`](./.github/PULL_REQUEST_TEMPLATE.md)** and **[`.github/ISSUE_TEMPLATE/`](./.github/ISSUE_TEMPLATE/)**: default templates inherited by every repo that doesn't override them.

## Reusable workflows

| Workflow | Purpose |
|---|---|
| `php-lint.yml` | PHPCS (WordPress Coding Standards) + PHPStan |
| `plugin-check.yml` | [WordPress Plugin Check](https://wordpress.org/plugins/plugin-check/) |
| `js-build.yml` | `npm ci && npm run build` and assert a `build/` artifact |

Example caller:

```yaml
jobs:
  php:
    uses: PlainPlugins/.github/.github/workflows/php-lint.yml@main
    with:
      php-version: "8.4"
  blocks:
    uses: PlainPlugins/.github/.github/workflows/js-build.yml@main
    with:
      node-version: "22"
  plugin-check:
    uses: PlainPlugins/.github/.github/workflows/plugin-check.yml@main
```

## License

GPL-2.0-or-later, same as every Plain Plugins plugin.
