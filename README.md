# GitHub-Actions

This is a collection of GitHub actions and workflows our staff uses routinely.

## Action Inventory

| Category | Item | Description |
| ---- | ---- | ---- |
| Terraform | [Terraform Docs](.github/actions/terraform-docs/README.md) | This action will use the [Terraform-docs](https://github.com/terraform-docs/terraform-docs/) package to generate Terraform documentation for all projects in the repository. |
|  | [Terraform Format](.github/actions/terraform-docs/README.md) | This action will use the [Terraform fmt](https://developer.hashicorp.com/terraform/cli/commands/fmt) utility to format all Terraform code in the repository. |

## Workflow Inventory
| Category | Item | Description |
| ---- | ---- | ---- |
| Terraform | [Code Checks](.github/workflows/codeChecks.yml) | Example of use for [Terraform Docs](.github/actions/terraform-docs/README.md) and  [Terraform Format](.github/actions/terraform-docs/README.md) | 