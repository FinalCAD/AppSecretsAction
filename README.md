# AppSecretsAction

Github Action to deploy in aws secret manager a set of secret from the app repository.
File should match this path `.finalcad/secrets.yaml`. You can find a list of all available keys on this [page](https://finalcad.atlassian.net/wiki/spaces/INFRA/pages/3213590529/Security+secrets)

## Inputs
### `app-name`
[**Required**] Application ID to identify the apps in eks-apps

### `aws-role`
[**Required**] AWS role allowing Secret manager usage

### `aws-region`
AWS region for ECR checks, Default: eu-central-1

### `terraform-version`
Terraform version to use, Default: latest

### `terragrunt-version`
Terragrunt version to use, Default: latest

### `appsecret-repo`
Repository containing terraform code for secret creation, Default: FinalCAD/terraform-app-secrets

### `appsecret-ref`
Reference to use for `appsecret-repo` repository, Default: master

### `github-ssh`
[**Required**] Github ssh key to pull `appsecret-repo` repository

### `environment`
[**Required**] Finalcad envrionment: production, staging, sandbox

### `region-friendly`
Finalcad region: frankfurt or tokyo, Default: frankfurt

### `secret-file`
Path for sercet file to create, Default: .finalcad/secrets.yaml

## Usage

```yaml
- name: Push secrets
  uses: FinalCAD/AppSecretsAction@v0.0.1
  with:
    github-ssh: ${{ secrets.GH_DEPLOY_SSH }}
    environment: sandbox
    region-friendly: frankfurt
    app-name: api1-service-api
    aws-role: ${{ secrets.DEPLOY_ROLE_MASTER }}
```
