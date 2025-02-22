# GitHub Actions - Copy Secrets

This repository contains a GitHub Actions workflow to copy secrets from one environment to another.

## Workflow

The workflow is defined in [`.github/workflows/copy_secrets.yml`](.github/workflows/copy_secrets.yml).

### Inputs

- `source`: The source environment from which to copy secrets.
- `destination`: The destination environment to which secrets will be copied.

### Permissions

- `contents: write`
- `id-token: write`

### Jobs

#### `copy_secrets`

- **Runs on**: `ubuntu-latest`
- **Steps**:
  1. **Checkout repository**: Uses `actions/checkout@v4.1.1` to checkout the repository.
  2. **Copy secrets**: Runs a PowerShell script to copy secrets from the source environment to a JSON file.
  3. **Upload secrets**: Uses `actions/upload-artifact@v2` to upload the JSON file containing the secrets.

## Usage

To trigger the workflow, use the `workflow_dispatch` event with the required inputs:

```yml
on:
  workflow_dispatch:
    inputs:
      source:
        type: environment
        description: 'Source environment'
        required: true
      destination:
        type: environment
        description: 'Destination environment'
        required: true