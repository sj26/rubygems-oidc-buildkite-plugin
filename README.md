# Rubygems OIDC Buildkite Plugin

Exchange a [Buildkite OIDC token] with [Rubygems] as a [trusted provider], via an [OIDC API Key Role], to securely push Rubygems from your Buildkite pipelines.

Is the exchange is successful, a short lifetime rubygems API Token will be
exported to the `GEM_HOST_API_KEY` environment variable. The `gem` cli tool
will detect and use that variable automatically.

Basic usage, which requires the `gem` command to be available in the agent environment:

```yaml
steps:
- label: ":rubygems: Build and push to Rubygems"
  plugins:
  - rubygems-oidc:
      role: rg_oidc_akr_...
  command: |
    gem build "*.gemspec"
    gem push "*.gem"
```

If the `gem` command is not available on the agents, this plugin can be combined with the `docker` plugin:

```yaml
steps:
- label: ":rubygems: Build and push to Rubygems"
  plugins:
    - rubygems-oidc:
        role: "rg_oidc_akr_..."
    - docker#v5.12.0:
        image: "ruby:slim"
        command: ["/bin/bash", "-c", "gem build *.gemspec && gem push *.gem"]
        environment:
          - GEM_HOST_API_KEY
```

[Buildkite OIDC token]: https://buildkite.com/docs/agent/v3/cli-oidc
[Rubygems]: https://rubygems.org
[trusted provider]: https://rubygems.org/profile/oidc/providers/2
[OIDC API Key Role]: https://rubygems.org/profile/oidc/api_key_roles

## Configuration

### Required

### `role` (required, string)

The `OIDC API Key Role` token provided by rubygems.org.

Example: `rg_oidc_akr_1a02be62783ebc2783ff`

### Optional

### `host` (optional, string)

The hostname to use when requesting a temporary API token from rubygems. Defaults to `https://rubygems.org` and only needs to be changed in testing situations.

Example: `https://example.com`

### `audience` (optional, string)

The audience to use when requesting an OIDC token from Buildkite. Defaults to `https://rubygems.org` and typically won't need to be customised.

Example: `example.com`

### `lifetime` (optional, string)

The number of seconds the requested Buildkite OIDC token will be valid for. Defaults to 60 seconds.

Example: `60`

## Thanks

Inspired by https://github.com/rubygems/configure-rubygems-credentials
