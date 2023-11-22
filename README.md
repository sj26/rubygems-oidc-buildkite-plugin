# Rubygems Buildkite OIDC support

Exchange a [Buildkite OIDC token] with [Rubygems] as a [trusted provider], via an [OIDC API Key Role], to securely push Rubygems from your Buildkite pipelines.

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
[OIDC API Key Role]: https://rubygems.org/profile/oidc/api_key_roles

## Thanks

Inspired by https://github.com/rubygems/configure-rubygems-credentials
