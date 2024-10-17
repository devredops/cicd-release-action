## Setting up this action for Ruby on Rails project

1. If you haven't already done so, create a `.github/workflows` folder in your
  repository (_this is where your actions will live_).
  ```shell
  mkdir -p .github/workflows
  ```

2. create a file named: `.release-please-manifest.json`, with the folloging content:
  ```json
  {
    ".": "0.0.0"
  }
  ```

3. create a file named: `.github/workflows/release-please-config.json`, with the folloging content:
  ```json
  {
    "release-type": "ruby",
    "bump-minor-pre-major": true,
    "bump-patch-for-minor-pre-major": true,
    "packages": {
      ".": {
        "version-file": "config/application.rb"
      }
    }
  }
  ```

2. Now create a `.github/workflows/release.yml` file with these contents:
  ```shell
  nano .github/workflows/release.yml
  ```
  with content:
  ```yaml
  name: release-please

  on:
    push:
      branches:
        - main

  permissions:
    contents: write
    pull-requests: write


  jobs:
    release-please:
      runs-on: ubuntu-latest

      steps:
        -
          uses: devredops/cicd-release-action@main
          id: release
          with:
            release-type: ruby
            version-file: config/application.rb
        -
          uses: devredops/cicd-build-push-on-gcp-action@main
          if: ${{ steps.release.outputs.release-created }}
          with:
            release-version: "${{ steps.release.outputs.release-version }}"
            gcr-auth-json:   "${{ secrets.GCLOUD_GCR_JSON_KEY }}"
            gcr-domain:      "${{ vars.GCR_DOMAIN }}"
            gcr-path:        "${{ vars.GCR_PROJECT }}/${{ github.repository }}"
  ```
