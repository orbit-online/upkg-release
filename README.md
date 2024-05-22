# upkg-install

A GitHub action to bundle a μpkg package and create a GitHub release with it

## Usage

```
name: Release

on:
  push:
    tags: ['v*']

jobs:
  release:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    name: Create GitHub release
    steps:
    - uses: orbit-online/upkg-release@v1
```

### Inputs

| Name                | Description                                                                                                       | Default                                                                                                             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `upkg-version`      | The version of μpkg to use for bundling                                                                           | The one already installed or `latest` (to always get `latest`, set this input explicitly)                           |
| `name`              | The name of the package, will override the name already set in `upkg.json`                                        | If `upkg.json` has no name: Name of the repository (without user/org prefix)                                        |
| `version`           | The version to write to `upkg.json`, corresponds to `-V` in `upkg bundle`                                         | [`program-version.sh "${{ github.ref }}"`](https://github.com/orbit-online/program-version), set to `""` to disable |
| `paths`             | Argument (space separated) list of relative paths to files and directories to include in the package.             | None, the μpkg default                                                                                              |
| `working-directory` | The working directory to change to before determining the version and bundling. This disables automatic checkout. | `.`                                                                                                                 |

### Outputs

| Name           | Description                                  |
| -------------- | -------------------------------------------- |
| `name`         | The name of the released package             |
| `version`      | The version of the released package          |
| `download-url` | The download URL of the released package     |
| `sha256`       | The SHA-256 checksum of the released package |
