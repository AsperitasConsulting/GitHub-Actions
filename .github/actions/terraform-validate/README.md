# Terraform Formatting Action

This action will use the [Terraform validate](https://developer.hashicorp.com/terraform/cli/commands/validate) utility to validate all Terraform projects in the repository.

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

            - name: Terraform Validate
              uses: AsperitasConsulting/GitHub-Actions/.github/actions/terraform-validate@v0.0.2

```

## Supported inputs

| Input Name | Type | Default | Description |
| --- | --- | --- | --- |
| ```version``` | ```string``` | ```1.8.0``` | Terraform version. |
