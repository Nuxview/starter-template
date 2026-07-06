# Starter Template

A minimalist, highly automated GitHub template repository designed to kickstart new projects with sensible defaults, built-in issue tracking, automatic Pull Request and Issue labeling, and automated changelog generation.

## 🚀 Features

- **GitHub Actions Workflows**:
  - 🏷️ **Auto PR & Issue Labeling (`.github/workflows/labels.yml`)**: Automatically labels Pull Requests and manages labels for Issues using the [actions/labeler](https://github.com/actions/labeler) GitHub Action.
  - 📝 **Automated Changelog (`.github/workflows/changelog.yml`)**: On merging a Pull Request into `main` or `master`, this workflow fetches the list of commits and changed files in the PR, formats a markdown entry, prepends it to [CHANGELOG.md](CHANGELOG.md), and commits the update back to the repository.
- **Issue Templates (`.github/ISSUE_TEMPLATE`)**: Includes pre-configured templates for [Bug Reports](.github/ISSUE_TEMPLATE/bug_report.md) and [Feature Requests](.github/ISSUE_TEMPLATE/feature_request.md) to standardize issue submissions.
- **Permissive License**: Pre-configured with the standard [MIT License](LICENSE).

---

## 🛠️ Getting Started

### 1. Create a Repository from this Template
Click the green **"Use this template"** button at the top of the repository page and choose **"Create a new repository"**.

### 2. Configure Workflow Permissions
The **Update Changelog on Merge** workflow needs permissions to push commits back to the repository. To enable this:
1. Navigate to your repository's **Settings** > **Actions** > **General**.
2. Scroll down to **Workflow permissions**.
3. Select **Read and write permissions**.
4. Check **"Allow GitHub Actions to create and approve pull requests"** (optional, but recommended if actions interact with PRs).
5. Click **Save**.

### 3. Add Labeler Rules (Optional)
The PR labeling workflow utilizes [actions/labeler](https://github.com/actions/labeler). To customize the labels applied to incoming PRs based on changed files, create a `.github/labeler.yml` file in your repository:
```yaml
# Example .github/labeler.yml configuration
frontend:
  - changed-files:
    - any-glob-to-any-file: 'src/frontend/**/*'
backend:
  - changed-files:
    - any-glob-to-any-file: 'src/backend/**/*'
documentation:
  - changed-files:
    - any-glob-to-any-file: 'docs/**/*'
    - any-glob-to-any-file: 'README.md'
```

---

## 📂 Project Structure

```text
.
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md       # Standardized bug reporting template
│   │   └── feature_request.md  # Standardized feature request template
│   └── workflows/
│       ├── changelog.yml       # Automates updates to CHANGELOG.md on PR merge
│       └── labels.yml          # Auto-labels Pull Requests and Issues
├── CHANGELOG.md                # Automatically updated release and change log
├── LICENSE                     # MIT License
└── README.md                   # Repository documentation (this file)
```

---

## 🔧 Workflow Details

### Update Changelog on Merge (`.github/workflows/changelog.yml`)
When a pull request is merged to `main` or `master`, this action:
1. Fetches all commit SHAs, dates, and messages in the pull request.
2. Identifies all changed files and their status (e.g., modified, added, deleted).
3. Generates a formatted release block containing the merge timestamp, PR author, merge commit, list of commits, and list of changed files.
4. Prepends the formatted entry to the top of `CHANGELOG.md` right after the header block separator (`---`).
5. Commits and pushes the change back to the repository using a retry mechanism to handle potential concurrency issues.

### Add Labels to PR & Issues (`.github/workflows/labels.yml`)
Runs whenever a pull request or issue is labeled or unlabeled, using the official `actions/labeler` action. It allows you to automatically classify PRs based on the path of the files changed.

---

## 📄 License

This repository is available as open source under the terms of the [MIT License](LICENSE).
