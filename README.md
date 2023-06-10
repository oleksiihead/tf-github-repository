# GitHub Repository Terraform Module

This Terraform module creates a private repository on GitHub, and adds a deploy key to it.

## Prerequisites
```bash
export TF_VAR_github_owner=<github_username>
export TF_VAR_github_token=<github_token>
export TF_VAR_public_key_openssh=$(cat ~/.ssh/id_rsa.pub)
export TF_VAR_public_key_openssh_title="Flux public key"
```

## Usage

```hcl
module "github_repository" {
  source                   = "github.com/oleksiihead/tf-github-repository"
  github_owner             = var.GITHUB_OWNER
  github_token             = var.GITHUB_TOKEN
  repository_name          = var.FLUX_GITHUB_REPO
  public_key_openssh       = module.tls_private_key.public_key_openssh
  public_key_openssh_title = "flux"
}
module "tls_private_key" {
  source = "github.com/oleksiihead/tf-hashicorp-tls-keys"
}
```
## Inputs
- github_owner - The name of the GitHub account that will own the repository.
- github_token - A GitHub personal access token with the repo scope.
- repository_name - (Optional) The name of the repository to create. Default is test-provider.
- repository_visibility - (Optional) The visibility of the repository. Default is private.
- branch - (Optional) The name of the branch to create. Default is main.
- public_key_openssh - The public key to use as a deploy key for the repository.
- public_key_openssh_title - The title of the public key to use as a deploy key for the repository.

## Outputs
- repository_name - The name of the created repository.

## Requirements
This module requires Terraform 0.13 or later, and the following provider:

github version >= 5.26.0

## License
This module is licensed under the MIT License. See the LICENSE file for details.
