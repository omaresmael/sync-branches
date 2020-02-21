# sync-branches

GitHub Action to sync one branch when another is updated.

## Inputs

### `GITHUB_TOKEN`

**Required** The token to be used for creating the pull request. Can be set to the one given for the workflow or another user.

### `FROM_BRANCH`

**Required** The branch you want to make the pull request from.

### `TO_BRANCH`

**Required** The branch you want to make the pull request to.

### `PULL_REQUEST_TITLE`

What you would like as the title of the pull request.

Default: `sync: {FROM_BRANCH} to {TO_BRANCH}`

### `PULL_REQUEST_BODY`

What you would like in the body of the pull request.

Default: `sync-branches: New code has just landed in {FROM_BRANCH} so let's bring {TO_BRANCH} up to speed!`

## Example usage

```YML
name: Sync
on:
  push:
    branches:
      - master

jobs:
  sync-branches:
    runs-on: ubuntu-latest
    name: Syncing branches
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Set up Node
        uses: actions/setup-node@v1
        with:
          node-version: 12
      - name: Opening pull request
        id: pull
        uses: tretuna/sync-branches@v1-beta.1
        with:
          GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}
          FROM_BRANCH: "master"
          TO_BRANCH: "develop"
```
