# Terraform Formatting Action

This action will use the [Terraform fmt](https://developer.hashicorp.com/terraform/cli/commands/fmt) utility to format all Terraform code in the repository.

# Usage

> Before calling this action, you must check out repository content.

## Example Workflow Usage
```yaml
name: Code Formatting

on:
    pull_request:
        types: ['opened', 'reopened', 'synchronize']
    workflow_dispatch:
        inputs:
            push:
              description: Push documentation changes
              required: true
              type: boolean
              default: true

jobs:
    format:
        name: format
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v4
              if: ${{ github.event_name == 'pull_request'}}
              with:
                ref: ${{ github.event.pull_request.head.ref }}

            - uses: actions/checkout@v4
              if: ${{ github.event_name != 'pull_request'}}

            - name: check formatting
              uses: AsperitasConsulting/GitHub-Actions/.github/actions/terraform-format@v0.0.1
              with:
                push: ${{ github.event_name == 'pull_request' || inputs.push }}

```

## Supported inputs

| Input Name | Type | Default | Description |
| --- | --- | --- | --- |
| ```push``` | ```boolean``` | ```false``` | If ```true```, pushes generated documentation changes back to the branch. |
| ```version``` | ```string``` | ```1.8.0``` | Terraform version. |
| ```gitUserName``` | ```string``` | ```github-actions[bot]``` | User name to use for git commit and push. |
| ```gitEmail``` | ```string``` | `````` | User email to use for git commit and push. |