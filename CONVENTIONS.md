# Plain Plugins: naming conventions

The single source of truth for how every Plain Plugins repository names things.

## The core idea: two identifiers, by context

Plain Plugins uses **two** identifiers, chosen by what the name is for.

1. **`plainplugins` / `PlainPlugins`** is the *vendor namespace*, used for **public, globally-registered** names that share a namespace with every other plugin on a site. Collision-safe. Used for: block names, pattern slugs, REST namespaces, PHP namespace root, Composer vendor.
2. **`plain_` / `PLAIN_` / `Plain_`** is the short *code prefix*, used for **internal code identifiers**. Used for: functions, classes, hooks, options, transients, CPT/taxonomy/meta keys, constants.

And one slug form:

3. **`plain-<feature>`** is an individual plugin's slug. This is the repo name, the plugin folder, and the text domain (all three identical, always).

> Why the split? `plain` alone is too generic for *registered* names. Another vendor could ship a `plain/` block or collide. `plainplugins` is unique, like `woocommerce/` or `jetpack/`. But for internal code identifiers, the short `plain_` prefix is fine and readable. There is **no `plain-plugins` (hyphenated) form** anywhere. Do not introduce one.

## Quick reference

Using `plain-example` as the canonical placeholder slug.

| Element | Convention | Example |
|---|---|---|
| **Repo / slug / text-domain** | `plain-<feature>` (the three are identical) | `plain-example` |
| **PHP namespace root** | `PlainPlugins\<Product>` (PascalCase, PSR-4) | `PlainPlugins\Example` |
| **Composer package** | `plainplugins/<full-plugin-slug>` | `plainplugins/plain-example` |
| **Block name** (`block.json` `name`) | `plainplugins/<block>` | `plainplugins/widget` |
| **Block context keys** | `plainplugins/<key>` | `plainplugins/cardIndex` |
| **Pattern slug** | `plainplugins/<pattern>` | `plainplugins/hero` |
| **REST namespace** | `plainplugins/v1` | `plainplugins/v1` |
| **PHP constants** | `PLAIN_<PRODUCT>_<NAME>` (product spelled out) | `PLAIN_EXAMPLE_VERSION` |
| **Functions** | `plain_<name>` (prefer OOP under the namespace) | `plain_render_widget()` |
| **Classes** (non-namespaced) | `Plain_<Name>` | `Plain_Engine` |
| **Hooks** (actions/filters) | `plain_<feature>_<event>` | `plain_example_sort_args` |
| **Options / transients** | `plain_<key>` | `plain_example_settings` |
| **CPT / taxonomy keys** | `plain_<key>` (CPT ≤ 20 chars, tax ≤ 32) | `plain_example_item` |
| **Post meta keys** | `plain_<key>`; protected/internal `_plain_<key>` | `_plain_example_priority` |
| **CSS auto block class** | `wp-block-plainplugins-<block>` (derived from block name) | `wp-block-plainplugins-widget` |
| **CSS BEM element/modifier** | `…__<element>`, `…--<modifier>` on the auto class | `wp-block-plainplugins-widget__item--active` |
| **JS global** | `plain` | `window.plain` |

## Rules

- Prefixes are 4+ chars and unique. Never use `wp_`, `_wp_`, `wc_`, `woo_`, `__`, or a bare leading `_` for your own identifiers.
- `Text Domain` must equal the plugin slug exactly (WordPress.org i18n requirement).
- The display name (`Plugin Name`) leads with "Plain": *Plain Example*.
- CPT keys are capped at 20 chars, taxonomy keys at 32.

## Plugin header

```php
/**
 * Plugin Name:       Plain Example
 * Version:           0.1.0
 * Requires at least: 7.0
 * Requires PHP:      8.4
 * License:           GPL-2.0-or-later
 * Text Domain:       plain-example
 *
 * @package PlainPlugins\Example
 */
```

## Migrating an existing name (breaking changes)

Renaming a **block name** or **CPT/taxonomy key** changes data that already lives in the database (stored block markup, the `post_type` column). Ship the rename in a coordinated migrator plugin that rewrites the stored data idempotently, rather than embedding migration code in the plugin itself. The plugin source stays migration-free.

Block **context keys** and **constants** are not persisted, so they need no migration. Rename provider and consumer together.
