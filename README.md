# Add Git-Hub PRs Comment

> A GitHub Action which adds a comment to a pull request's issue. This is usefull in Post Terraform Plan or Terraform Apply outputs to the GitHub PRs.

## Usage

```yaml
on:
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: Adarsh-Suvarna/GitHub-PR-Comment@v1.0.1
        with:
          message: |
            **Hello**
          repo-token: ${{ secrets.GITHUB_TOKEN }}
          repo-token-user-login: 'github-actions[bot]'
          allow-repeats: false
```

This can be even use it on PR Issues that are related to PRs that were merged into master.

```yaml
on:
  push:
    branches:
      - master

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: Adarsh-Suvarna/GitHub-PR-Comment@v1.0.1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          message: |
            **Hello MASTER**
          allow-repeats: true
```

## Configuration options

| Variable or Argument  | Location | Description                                                                                                                 | Required | Default |
| --------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------- | -------- | ------- |
| message               | with     | The message you'd like displayed, supports Markdown and all valid Unicode characters                                        | yes      |         |
| repo-token            | with     | A valid GitHub token, either the temporary token GitHub provides or a personal access token                                 | maybe    |         |
| repo-token-user-login | with     | Define this to save on comment processing time when checking for repeats. GitHub's default token uses `github-actions[bot]` | no       |         |
| allow-repeats         | with     | A boolean flag to allow identical messages to be posted each time this action is run                                        | no       | false   |
| proxy-url             | with     | A string for your proxy service URL if you'd like this to work with fork-based PRs                                          | no       |         |
| GITHUB_TOKEN          | env      | A valid GitHub token, can alternatively be defined in the env                                                               | no    |         |