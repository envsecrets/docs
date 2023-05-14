---
description: >-
  Setup and usage guide on how to continuously sync your secrets with GCP
  Secrets Manager.
---

# GCP Secrets Manager

## Prerequisites

* You have a [GCP account](https://console.cloud.google.com/) and are familiar with GCP Secret Manager
* You have the [gcloud CLI](https://cloud.google.com/sdk/docs/install) installed and authenticated
* You have [enabled the Secret Manager API](https://console.cloud.google.com/apis/library/secretmanager.googleapis.com) for your GCP project

{% hint style="info" %}
Ensure the gcloud CLI is configured to use the correct project, e.g. `gcloud config set project [your-project]` before proceeding.
{% endhint %}

## Setup

1.  **Create new IAM Service Account**



    Run the following commands with the **gcloud** CLI.



    ```bash
    # To narrow permission scope use this prefix for envsecrets accessible secrets.
    SECRET_PREFIX="envsecrets-";

    # Get current project
    PROJECT_ID="$(gcloud config get-value project --quiet)";

    # Create a new Service Account
    gcloud iam service-accounts create envsecrets \
      --description="Service account for envsecrets to sync secrets to Secret Manager" \
      --display-name="envsecrets";

    # Attach SecretManagerAdmin policy to the new service account
    gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member="serviceAccount:envsecrets@$PROJECT_ID.iam.gserviceaccount.com" \
      --role="roles/secretmanager.admin" \
      --condition="expression=resource.name.extract(\"secrets/{rest}\").startsWith(\"$SECRET_PREFIX\"),title=\"$SECRET_PREFIX*\"";

    ```


2.  **Create keys for the new service account**



    ```bash
    # Generate a key for your new service account
    gcloud iam service-accounts keys create iam-key.json \
      --iam-account="envsecrets@$PROJECT_ID.iam.gserviceaccount.com";

    # Print (and then remove) the JSON credentials
    cat iam-key.json && rm iam-key.json;
    ```

    &#x20;

    Copy and save the keys printed on your shell.


3. **Configuration**
   1. Go to [integrations catalog](https://app.envsecrets.com/integrations/catalog) in your envsecrets dashboard and choose "GCP Secrets Manager."
   2. On the setup/connection page, enter the service account keys you created above and save the form.

{% hint style="info" %}

{% endhint %}

## Activation

1. Go to the [integrations](https://app.envsecrets.com/integrations) dashboard in your envsecrets organisation and under "GCP Secrets Manager" choose "Manage."
2. Click on "Sync Secrets" button.
3. In the page that opens, select your envsecrets project, environment and enter the name with which you wish you save your secret in GCP Secrets Manager.
4. Complete and save the form.

## Usage

1. Right after saving the configuration and activating an integration on a specific environment in envsecrets, your secrets will automatically get synced for the first time to your GCP Secrets Manager. It is advisable you open your GCP dashboard and check the values in your new secret.
2. From here on, every time you create a new version of your secrets in your environment, the new values will automatically get pushed to your GCP secret.

{% hint style="warning" %}
Every new version of your secret in envsecrets will create a new version of the existing secret in GCP Secrets Manager.
{% endhint %}
