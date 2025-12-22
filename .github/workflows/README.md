# Automated Version Update Workflow

This repository contains a GitHub Actions workflow that automatically creates a PR when a new version of Coot is released.

## Features

- Checks upstream Coot repository daily at 00:00 UTC
- Automatically updates manifest file when new release is detected
- Supports creating PRs to Flathub repository
- Can be triggered manually

## Setup Instructions

### Option 1: Create PR directly to Flathub (Recommended)

To create PRs directly to the Flathub repository (`flathub/io.github.pemsley.coot`):

1. **Create a Personal Access Token:**
   - Navigate to: GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - Select the following scopes:
     - `repo` (full access)
     - `workflow`
   - Generate the token and copy it to a safe place

2. **Add as Repository Secret:**
   - Navigate to: This repository's Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `FLATHUB_PAT`
   - Secret: Paste the PAT you created
   - Click "Add secret"

3. **Done!** The workflow will automatically create PRs to Flathub

### Option 2: Create PR in local repository

If FLATHUB_PAT is not configured, the workflow will create a PR in this repository. You can then manually create a PR to Flathub.

No additional setup required. The workflow will work automatically.

## Usage

### Automatic Execution

The workflow runs automatically every day at 00:00 UTC. When a new version is detected, a PR is automatically created.

### Manual Execution

You can manually trigger the workflow for testing or immediate checks:

1. Navigate to the "Actions" tab
2. Select "Update Coot Version" workflow
3. Click "Run workflow"
4. Select branch and click "Run workflow"

## Workflow Details

The workflow performs the following steps:

1. **Version Check**
   - Fetches latest release from upstream Coot repository
   - Compares with current version in manifest

2. **If Update is Needed**
   - Updates tag in manifest file (`io.github.pemsley.coot.yaml`)
   - Commits changes
   - Creates PR (to Flathub or locally)

3. **PR Content**
   - Title: "Update Coot to [version]"
   - Includes changes and link to upstream release
   - Automatically labeled with `automated` and `version-update`

## Troubleshooting

### PR is not created

- Check workflow logs for errors
- Verify upstream repository has published new releases
- Verify FLATHUB_PAT is correctly configured (for Flathub PR creation)

### Workflow does not run

- Verify GitHub Actions is enabled for the repository
- Verify workflow file is in correct path (`.github/workflows/`)

## License

This workflow follows the repository's license.
