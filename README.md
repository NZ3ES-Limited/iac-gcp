# gcp-iac

Infrastructure as Code on GCP

## Prerequisites (bootstrap)

- create storage account
    gcloud --project=iac-01 storage buckets create gs://nz3es-tf-state-iac --location=australia-southeast2

- enable versioning on bucket
    gcloud storage buckets update gs://nz3es-tf-state-iac --enable-versioning

- create IAM service account
    gcloud iam service-accounts create nz3es-automation-sa \
    --description="SA for automation" \
    --display-name="nz3es-automation-sa" \
    --project=iac-01

- Create a service account key
    gcloud iam service-accounts keys create nz3es-automation-sa-key.json \
    --iam-account=<nz3es-automation-sa@iac-01.iam.gserviceaccount.com> \
    --project=iac-01

- Enable Infra Manager executes Terraform using the identity of this service account.
    gcloud services enable config.googleapis.com --project=iac-01
        Operation "operations/acf.p2-834266050147-7660ac92-75e4-411f-9b2d-412081eb3dd7" finished successfully.

    gcloud services enable cloudquotas.googleapis.com --project=iac-01

    gcloud projects add-iam-policy-binding iac-01 \
        --member="serviceAccount:nz3es-automation-sa@iac-01.iam.gserviceaccount.com" \
        --role="roles/config.agent" \
        --project=iac-01

- Adding required roles to the service account
    gcloud projects add-iam-policy-binding iac-01 \
        --member="serviceAccount:nz3es-automation-sa@iac-01.iam.gserviceaccount.com" \
        --role="roles/compute.networkAdmin" \
        --project=iac-01

        --role="roles/compute.instanceAdmin.v1"
        --role="roles/iam.serviceAccountUser"
        --role="roles/container.admin"
        --role="roles/bigquery.admin"
        --role="roles/storage.admin"
        --role="roles/serviceusage.serviceUsageAdmin"
