# terraform_state_artifact_gcs_backend
The [`European-Camping-Group-Data-Team/terraform_state_artifact_gcs_backend`](https://github.com/European-Camping-Group-Data-Team/terraform_state_artifact_gcs_backend) action is a composite action that stores your Terraform state using the google backend. Built-in are the actions: [`hashicorp/setup-terraform@v4`](https://github.com/hashicorp/setup-terraform).

## :rocket: What this action does: :rocket:

- 🛠️ It installs terraform using [`hashicorp/setup-terraform@v4`](https://github.com/hashicorp/setup-terraform).
- :building_construction: If no apply action is defined it runs `terraform plan` with any flags from the optional variable `custom_plan_flags`
- 🏢 Next it runs `terraform apply` with any flags from the optional variable`custom_apply_flags`.
  - This can be skipped by setting the optional variable `apply` to `false`.
- 🗃️ If all is well then Terraform has now produced a statefile `./terraform.tfstate`.

## Usage v1

```yaml
steps:
- uses: European-Camping-Group-Data-Team/terraform_state_artifact_gcs_backend@v1
    with:
        environment: 'dev'
```

You can choose to skip `terraform apply`:

```yaml
steps:
- uses: European-Camping-Group-Data-Team/terraform_state_artifact_gcs_backend@v1
    with:
        environment: 'dev'
        apply: false
        terraformstatefile: 'terraformstatefile-dev'
```

You can choose to add custom flags to `terraform plan`:

```yaml
steps:
- uses: European-Camping-Group-Data-Team/terraform_state_artifact_gcs_backend@v1
    with:
        environment: 'dev'
        apply: false
        custom_plan_flags: '-refresh-only'
        terraformstatefile: 'terraformstatefile-dev'
```

You can choose to add custom flags to `terraform apply`:

```yaml
steps:
- uses: European-Camping-Group-Data-Team/terraform_state_artifact_gcs_backend@v1
    with:
        environment: 'dev'
        custom_apply_flags: '-no-color'
        terraformstatefile: 'terraformstatefile-dev'
```

## Inputs v1

The action supports the following inputs:

| Variable        | Description                                                                                                                             | Default |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------|
value.                                              |   N/A   |
| `environment`         | Environment to use (dev, staging or prod).               | N/A  |
| `upload`         | (optional) Upload a statefile to GCS.               | `false`  |
| `apply`         | (optional) Whether to run the `terraform apply` command.               | `true`  |
| `destroy`       | (optional) Whether to run the `terraform apply -destroy` command.               | `false`  |
| `upload`         | (optional) Upload artifact file.               | `false`  |
| `custom_plan_flags`         | (optional) Add a custom flag to the `terraform plan` command.               | `''`  |
| `custom_apply_flags`         | (optional) Add a custom flag to the `terraform apply` command.               | `''`  |
| `custom_destroy_flags`         | (optional) Add a custom flag to the `terraform apply -destroy` command.               | `''`  |
