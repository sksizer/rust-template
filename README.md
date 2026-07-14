# Rust Template [![Github Actions][gha-badge]][gha] [![License: MIT][license-badge]][license]

[gha]: https://github.com/PaulRBerg/rust-template/actions
[gha-badge]: https://github.com/PaulRBerg/rust-template/actions/workflows/ci.yml/badge.svg
[license]: https://opensource.org/licenses/MIT
[license-badge]: https://img.shields.io/badge/License-MIT-blue.svg

A template for developing Rust projects, with sensible defaults.

## Getting Started

Click the [`Use this template`](https://github.com/PaulRBerg/rust-template/generate) button at the top of the page to
create a new repository with this repo as the initial state.

## Features

### Sensible Defaults

This template comes with sensible default configurations in the following files:

```text
├── .editorconfig
├── .gitignore
├── .prettierrc.yml
├── Cargo.toml
├── justfile
└── rustfmt.toml
```

### GitHub Actions

This template comes with GitHub Actions pre-configured. Your code will be linted and tested on every push and pull
request made to the `main` branch.

You can edit the CI script in [.github/workflows/ci.yml](./.github/workflows/ci.yml).

### Automated Releases

Releases are automated by [release-plz](https://release-plz.dev/): on every push to `main`, a bot opens (or updates) a
`chore: release` PR with the version bump and changelog. Merging that PR tags the release, publishes to crates.io, and
creates a GitHub Release. See [RELEASE.md](./RELEASE.md) for the full flow.

Two one-time setup steps are required in each new repository created from this template:

1. **Set the crates.io token** so the publish step can run. Create an API token at
   [crates.io/settings/tokens](https://crates.io/settings/tokens) (scope: `publish-new` + `publish-update`), then:

   ```sh
   gh secret set CARGO_REGISTRY_TOKEN
   ```

   (Paste the token when prompted, or pipe it in. Without this secret, the release PR still gets opened — only the
   crates.io publish on merge will fail.)

2. **Allow GitHub Actions to create pull requests** — GitHub disables this by default, and release-plz can't open the
   release PR without it. Enable it under Settings → Actions → General → Workflow permissions, or via CLI:

   ```sh
   gh api -X PUT repos/<owner>/<repo>/actions/permissions/workflow \
     -f default_workflow_permissions=read -F can_approve_pull_request_reviews=true
   ```

If the project should not be published to crates.io, set `publish = false` in
[release-plz.toml](./release-plz.toml) — you keep the automated versioning, changelog, tags, and GitHub Releases.

## Usage

See [The Rust Book](https://doc.rust-lang.org/book/) and [The Cargo Book](https://doc.rust-lang.org/cargo/index.html).

## License

This project is licensed under MIT.
