# sx Assets Vault

This repository serves as an sx vault for AI assets (skills, commands, MCPs).

## Usage

Configure sx to use this vault:

```bash
sx init --type git --repo-url git@github.com:ealt/sx-assets.git
```

Then browse and install assets:

```bash
sx vault list
sx add <asset-name> --yes --scope-global
sx install
```

## Asset Sources

Assets are authored in [ealt/toolchain](https://github.com/ealt/toolchain) and
published here via `sx add`.
