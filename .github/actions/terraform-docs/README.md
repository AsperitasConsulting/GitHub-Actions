# Terraform Documentation Generator Action

This action will use the [Terraform-docs](https://github.com/terraform-docs/terraform-docs/) package to generate Terraform documentation for all projects in the repository.

# Usage

> A Terraform-docs configuration file (e.g. ```.terraform-docs.yml```) must be present.

Either place your Terraform-docs configuration file (```.terraform-docs.yml```) in the root of the repository *or* place one in every Terraform project in the repository.

> Before calling this action, you must check out repository content.

## Example Workflow Usage
```yaml
name: Code Documentation

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
    docs:
        name: docs
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v4
              if: ${{ github.event_name == 'pull_request'}}
              with:
                ref: ${{ github.event.pull_request.head.ref }}

            - uses: actions/checkout@v4
              if: ${{ github.event_name != 'pull_request'}}

            - name: check docs
              uses: AsperitasConsulting/GitHub-Actions/.github/actions/terraform-docs@v0.0.1
              with:
                push: ${{ github.event_name == 'pull_request' || inputs.push }}
```

## Supported inputs

| Input Name | Type | Default | Description |
| --- | --- | --- | --- |
| ```push``` | ```boolean``` | ```false``` | If ```true```, pushes generated documentation changes back to the branch. |
| ```config``` | ```string``` | ```.terraform-docs.yml``` | Terraform Docs config file. |
| ```gitUserName``` | ```string``` | ```github-actions[bot]``` | User name to use for git commit and push. |
| ```gitEmail``` | ```string``` | `````` | User email to use for git commit and push. |