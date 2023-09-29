# LCOV Report Comment Generator
Action for reporting LCOV code coverage on pull requests

# Sample Report

## LCOV Report - Todo App ✅
### All Files
- Lines: 1440/1842 (78.2%) ✅ (Minimum coverage is 70%)
- Functions: N/A
- Branches: N/A

### Changed Files
- Lines: 50/50 (100.0%) ✅ (Minimum coverage is 90%)
- Functions: N/A
- Branches: N/A

| File              | Lines          | Functions | Branches |
| ----------------- | -------------- | --------- | -------- |
| app_user.dart     | 7/7 (100.0%)   | N/A       | N/A      |
| cart_service.dart | 43/43 (100.0%) | N/A       | N/A      |

# Usage
```yml
- uses: boris-amenitiz/lcov-pull-request-report@v1.0.0
  with:
    # Lcov file location. For example, coverage/lcov.info
    lcov-file: coverage/lcov.info

    # Github token required for getting list of changed files and posting comments
    github-token: ${{ secrets.GITHUB_TOKEN }}

    # Working directory
    # Default: empty (repository root)
    working-directory:

    # Report comment title
    # Default: empty
    comment-title:

    # All files minimum coverage in percentage. For example, 0, 50, 100
    # Default: 0
    all-files-minimum-coverage:

    # Changed files minimum coverage in percentage. For example, 0, 50, 100
    # Default: 0
    changed-files-minimum-coverage:

    # Artifact name of the generated html. Requires LCOV to be installed
    # Default: empty (skip uploading artifact)
    artifact-name:
```

# Permissions

Write permission must be given for writing pull request comment. There are 2 ways:
- Enable "Read and write permissions" in Repository Settings > Code and automation > Actions > General > Workflow permissions, or
- Add `permissions: write-all` to the job. See https://docs.github.com/en/actions/using-jobs/assigning-permissions-to-jobs

## Outputs

By default, action attaches comment to a pull request. However, if you want to use other action for publishing report, you can use the output as it follows:

```yaml
- uses: boris-amenitiz/lcov-pull-request-report@v1.0.0
    # give the id for the step, to access outputs in another step.
    id: coverage

- uses: marocchino/sticky-pull-request-comment@v2
    with:
      # pass output from the previous step by id.
      message: ${{ steps.coverage.outputs.report }}
```

Also, you can use this data on other platforms. For instance, you can send report to your [Slack](https://github.com/slackapi/slack-github-action) or [Jira](https://github.com/atlassian/gajira-comment).


# License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
