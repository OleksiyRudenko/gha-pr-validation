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

## Resources

- [GH action: Labeler](https://github.com/actions/labeler)
- [GH action: Paths Changes Filter](https://github.com/RasaHQ/pr-changed-files-filter)
- [How to enforce good Pull Requests on Github](https://www.vantage-ai.com/blog/how-to-enforce-good-pull-requests-on-github)
