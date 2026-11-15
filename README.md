# GitHub state package
## Why you'd want this

GitHub state at hand: accounts, organizations and repositories cached locally for offline reads, with live identity verification before any write.

- No token ceremony per question — account/org/repo facts are pre-cached with TTL context
- Writes stay honest: identity and permission are verified live before anything changes
- Zero credentials in the cache; the connector and the cache are separate faces


Cache selected GitHub account, organization, repository and gh environment facts for agents. Read cached context offline; refresh explicitly when current state is needed.

Package: github 0.1. Framework: >= 0.3. Python: >= 3.9. System connector: official gh >= 2.0, authenticated by the human. No connector executable or credentials are shipped.

## Local development installation

From a separate framework instance:

```text
python .owfa/scripts/owfa_kernel.py install github --path /path/to/pkg-github
python .owfa/scripts/owfa_kernel.py validate --scope github
python .owfa/scripts/owfa_kernel.py all
python .owfa/plugins/domains/github/github/scripts/state.py show --account LOGIN
python .owfa/plugins/domains/github/github/scripts/state.py refresh --account LOGIN --repo OWNER/REPO
```

Source layout: `PKG.yaml`, `github/` (domain manifest and scripts), `command/github-state/` (skill), `docs/` (review documentation). Installation lands the package at `.owfa/plugins/domains/github/`; do not wrap this repository inside another domains/github directory.

See [docs/github-domain.md](docs/github-domain.md) for design and [docs/github-validation.md](docs/github-validation.md) for evidence and limitations. The complete domain contract lives in [github/PLUGIN.md](github/PLUGIN.md).

This package does not change GitHub resources, make login permanent or use cached permissions as authorization. Snapshots stay in the user's instance. No September kernel-reliability changes are included.
