## Summary

<!-- One or two lines: what changes and why. -->

## Convention checklist

<!-- Tick what applies; see https://github.com/PlainPlugins/.github/blob/main/CONVENTIONS.md -->

- [ ] Slug, repo name, and text-domain are identical (`plain-<feature>`)
- [ ] Constants spell out the product (`PLAIN_<PRODUCT>_*`)
- [ ] New hooks use `plain_<product>_*` (no abbreviations)
- [ ] Block names use `plainplugins/<block>`
- [ ] CPT/taxonomy/meta keys use `plain_<key>` (or `_plain_<key>` for protected meta)
- [ ] Migrations (if any) live in `plain-plugins-migrator`, not in this plugin's source

## Test plan

<!-- Steps to verify. CI covers lint + build; describe manual checks. -->
