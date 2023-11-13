# Rubygems Buildkite OIDC support

Exchange a Buildkite OIDC token for a Rubygems API token, to securely push Rubygems from your Buildkite pipelines.

```yaml
steps:
- label: ":rubygems: Build and push to Rubygems"
  plugins:
  - rubygems-oidc:
      role: rg_oidc_akr_...
  command: |
    gem build "*.gem"
    gem push "*.gem"
```

## Thanks

Inspired by https://github.com/rubygems/configure-rubygems-credentials
