# Rubygems Buildkite OIDC support

> [!NOTE]
> This is not yet generally available, but [work is in progress](https://github.com/rubygems/rubygems.org/pull/4159).

Exchange a [Buildkite OIDC token] for a [Rubygems] API token, as a [trusted provider], to securely push Rubygems from your Buildkite pipelines.

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

[Buildkite OIDC token]: https://buildkite.com/docs/agent/v3/cli-oidc
[Rubygems]: https://rubygems.org
[trusted provider]: https://rubygems.org/profile/oidc/providers/2

## Thanks

Inspired by https://github.com/rubygems/configure-rubygems-credentials
