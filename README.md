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
        fromLocal: true
        fromFork: true
        byall: true
        bycontributor: false
        # {{prOpenerName}} will be replaced with a PR opener username
        allowfileschange: [ 'submissions/{{prOpenerName}}/*/*.{js|html|css|scss}' ]
        maxfileschanged: 3
        # runs lintercommand against allowed files (if set to true) or against specified filepath(s)
        runlinter: false
        lintercommand: null
        checkcompetingprs: true
        labelsize: true
        onsuccess: 'No issues detected. This doesn't mean there are not any. You may want to check [files](./files) for thorough checks.\n\n{{summary}}'
        onfailure: 'There are {{issuesCount}} issue(s) detected.\n\n{{summary}}\n\n<details><summary>CLICK ME</summary>\n<p>\n\n{{detailsPerFile}}\n\n</p></details>'
        # you need the following labels being defined on the targeted repo
        labelsuccess: pr-validation-passed
        labelfailure: pr-validation-failed
        labeldisable: pr-validation-disabled
        labelxs: XS
        labels: S
        labelm: M
        labell: L
        labelxl: XL
```

## Resources

- [GH action: Labeler](https://github.com/actions/labeler)
- [GH action: Paths Changes Filter](https://github.com/RasaHQ/pr-changed-files-filter)
- [How to enforce good Pull Requests on Github](https://www.vantage-ai.com/blog/how-to-enforce-good-pull-requests-on-github)
