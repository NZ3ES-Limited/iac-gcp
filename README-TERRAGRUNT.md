# Terragrunt quick start (supplementary)

This file explains how to use the Terragrunt skeleton in this repo without modifying the main README.

1) Ensure credentials and project are set:

    ```bash
    export GOOGLE_APPLICATION_CREDENTIALS="/path/to/service-account.json"
    export GCP_PROJECT_ID="your-gcp-project-id"
    export GCP_REGION="<region>"
    ```

2) Create and configure a GCS bucket for state and enable versioning.
3) Update `terragrunt.hcl` at repo root: set `remote_state.config.bucket` to your bucket name.
4) Run from an environment folder, e.g.: `live/<env>/<region>`:

```bash
cd live/<env>/<region>
terragrunt init
terragrunt plan
terragrunt apply
```

- Enable debug log if required
  - TG_LOG_LEVEL=DEBUG terragrunt init
