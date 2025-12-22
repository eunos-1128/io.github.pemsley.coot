# Automated Version Update Workflow

このリポジトリには、Cootの新しいバージョンがリリースされた際に自動的にPRを作成するGitHub Actionsワークフローが含まれています。

This repository contains a GitHub Actions workflow that automatically creates a PR when a new version of Coot is released.

## 機能 / Features

- 毎日午前0時（UTC）に上流のCootリポジトリをチェック / Checks upstream Coot repository daily at 00:00 UTC
- 新しいリリースを検出すると自動的にmanifestファイルを更新 / Automatically updates manifest file when new release is detected
- FlathubリポジトリへのPR作成をサポート / Supports creating PRs to Flathub repository
- 手動実行も可能 / Can be triggered manually

## セットアップ方法 / Setup Instructions

### オプション1: Flathubへ直接PRを作成（推奨） / Option 1: Create PR directly to Flathub (Recommended)

Flathubリポジトリ（`flathub/io.github.pemsley.coot`）へ直接PRを作成するには：

To create PRs directly to the Flathub repository (`flathub/io.github.pemsley.coot`):

1. **Personal Access Token (PAT) の作成 / Create a Personal Access Token:**
   - GitHubの Settings → Developer settings → Personal access tokens → Tokens (classic) へ移動
   - "Generate new token (classic)" をクリック
   - 以下のスコープを選択：
     - `repo` (フルアクセス)
     - `workflow`
   - トークンを生成して安全な場所にコピー

   Navigate to: GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - Select the following scopes:
     - `repo` (full access)
     - `workflow`
   - Generate the token and copy it to a safe place

2. **リポジトリのSecretに追加 / Add as Repository Secret:**
   - このリポジトリの Settings → Secrets and variables → Actions へ移動
   - "New repository secret" をクリック
   - Name: `FLATHUB_PAT`
   - Secret: 作成したPATを貼り付け
   - "Add secret" をクリック

   Navigate to: This repository's Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `FLATHUB_PAT`
   - Secret: Paste the PAT you created
   - Click "Add secret"

3. **完了！ワークフローが自動的にFlathubへPRを作成します / Done! The workflow will automatically create PRs to Flathub**

### オプション2: ローカルリポジトリでPRを作成 / Option 2: Create PR in local repository

FLATHUB_PATを設定しない場合、ワークフローはこのリポジトリ内にPRを作成します。その後、手動でFlathubへPRを作成できます。

If FLATHUB_PAT is not configured, the workflow will create a PR in this repository. You can then manually create a PR to Flathub.

追加の設定は不要です。ワークフローは自動的に動作します。

No additional setup required. The workflow will work automatically.

## 使用方法 / Usage

### 自動実行 / Automatic Execution

ワークフローは毎日午前0時（UTC）に自動的に実行されます。新しいバージョンが検出されると、自動的にPRが作成されます。

The workflow runs automatically every day at 00:00 UTC. When a new version is detected, a PR is automatically created.

### 手動実行 / Manual Execution

テストや即座の確認のため、手動でワークフローを実行できます：

You can manually trigger the workflow for testing or immediate checks:

1. このリポジトリの "Actions" タブへ移動 / Navigate to the "Actions" tab
2. "Update Coot Version" ワークフローを選択 / Select "Update Coot Version" workflow
3. "Run workflow" をクリック / Click "Run workflow"
4. ブランチを選択して "Run workflow" をクリック / Select branch and click "Run workflow"

## ワークフローの詳細 / Workflow Details

ワークフローは以下のステップを実行します：

The workflow performs the following steps:

1. **バージョンチェック / Version Check**
   - 上流のCootリポジトリから最新リリースを取得 / Fetches latest release from upstream Coot repository
   - 現在のmanifestファイルのバージョンと比較 / Compares with current version in manifest

2. **更新が必要な場合 / If Update is Needed**
   - manifestファイル（`io.github.pemsley.coot.yaml`）のtagを更新 / Updates tag in manifest file
   - 変更をコミット / Commits changes
   - PRを作成（Flathubまたはローカル） / Creates PR (to Flathub or locally)

3. **PR内容 / PR Content**
   - タイトル: "Update Coot to [version]"
   - 変更内容と上流リリースへのリンクを含む / Includes changes and link to upstream release
   - `automated` と `version-update` ラベルを自動付与 / Automatically labeled with `automated` and `version-update`

## トラブルシューティング / Troubleshooting

### PRが作成されない / PR is not created

- ワークフローログを確認してエラーを確認 / Check workflow logs for errors
- 上流リポジトリが新しいリリースを公開しているか確認 / Verify upstream repository has published new releases
- FLATHUB_PATが正しく設定されているか確認（Flathub PR作成時） / Verify FLATHUB_PAT is correctly configured (for Flathub PR creation)

### ワークフローが実行されない / Workflow does not run

- リポジトリでGitHub Actionsが有効になっているか確認 / Verify GitHub Actions is enabled for the repository
- ワークフローファイルが正しいパスにあるか確認（`.github/workflows/`） / Verify workflow file is in correct path (`.github/workflows/`)

## ライセンス / License

このワークフローはリポジトリのライセンスに従います。

This workflow follows the repository's license.
