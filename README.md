# GitHub Action: Generate Release

This GitHub Action automates the process of generating a new release based on the specified release type and version file.

## Inputs:
- **`config-file`** (required):  
  Defines the release strategy for the repository (e.g., `sample`, `node`, `python`, `ruby`). For more details, refer to the [Release types supported](https://github.com/googleapis/release-please-action#release-types-supported).

## Outputs:
- **`release-created`**:  
  A boolean (`true` or `false`) indicating whether a release was successfully created.

- **`release-version`**:  
  The version number generated for the release (e.g., `1.2.3`).

## Important Note:
This action is based on [Google's Release Please Action](https://github.com/googleapis/release-please-action). For more comprehensive documentation, refer to the official repository.

After integrating this action into your repository, ensure that new commits follow the [Conventional Commits](https://www.conventionalcommits.org/) convention. By doing so, [release-please](https://github.com/googleapis/release-please) will automatically start creating Release PRs for you.

---

## Setting Up This Action
This project includes several useful resources to help you get started:
  - [Ruby on Rails Project](./docs/ruby-on-rails.md)

---
