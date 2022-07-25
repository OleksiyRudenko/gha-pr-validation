# gha-pr-validation
GitHub action to provide pull request validation

Features:
- Allowed pathname patterns (may include depth restrictions, submitter's username) + label when disallowed file types added
- Makes sure that certain part of pathnames is same across all files (helpful to avoid mixing up with other PRs)
- Checks if other PR contains some of the changes already
- Files count, bytesize and LOC changed count metrics for warnings 
- Files in PR stats: count, bytesize, LOCs count, LOCs changed, changes percentage
- Labeler GHA to label PR size: XS through XL
- Per file stats (in a foldable section): pathname, bytesize, LOC count, LOC changed
- Runs on every PR update

## Table of contents


## Usage examples

```yml
name: PR static validation
on:
  - pull_request_target
    branches:
      - main
jobs:
  validate:
      - uses: oleksiyrudenko/gha-pr-validation@v1-latest
        with:
          token: '${{ secrets.GITHUB_TOKEN }}'
          # Applied to PRs opened locally and/or from a fork
          fromLocal: true
          fromFork: true
          # Applied to PRs opened by user categories (anyone, contributors, explicit list of users)
          byAll: true
          byContributors: false
          byUsers: null
          # What files are allowed on a PR {{prOpenerName}} will be replaced with a PR opener username
          allowFilesPaths: [ 'submissions/{{prOpenerName}}/*/*.{js|html|css|scss}' ]
          # To what depth filepaths should be identical
          pathIdentityDepth: 3
          # Max number of changed files allowed
          maxFilesChanged: 3
          # Checks if other PRs suggest changes to the same files as current PR (warning)
          checkCompetingPRs: true
          # Reporting templates
          onSuccess: 'No issues detected. This doesn't mean there are not any. You may want to check [files](./files) for thorough checks.\n\n{{summary}}'
          onFailure: 'There are {{issuesCount}} issue(s) detected.\n\n{{summary}}\n\n<details><summary>CLICK ME</summary>\n<p>\n\n{{detailsPerFile}}\n\n</p></details>'
          # Labels to apply based on status
          # - you need the following labels being defined on the targeted repo
          labelSuccess: pr-validation-passed
          labelFailure: pr-validation-failed
          # - disables validation checks when assigned on a PR
          labelDisabled: pr-validation-disabled
```

## Helpful Related Resources and GitHub Actions

- [How to enforce good Pull Requests on Github](https://www.vantage-ai.com/blog/how-to-enforce-good-pull-requests-on-github)
- [GH action: Labeler](https://github.com/actions/labeler) can autolabel PRs
- [GH action: Prettier](https://github.com/marketplace/actions/prettier-action) can style code or highlight issues with code styling
- [GH action: Size Label](https://github.com/pascalgn/size-label-action) can add labels based on changes size
- [GH action: Paths Changes Filter](https://github.com/RasaHQ/pr-changed-files-filter)
  enables conditional execution of workflow steps and jobs, based on the files modified by pull request, feature branch or in pushed commits
