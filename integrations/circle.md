---
description: Setup and usage guide on how to continuously sync your secrets with Circle CI.
---

# Circle CI

## Setup

1. **Generate your Personal Access Token**
   1. Go to [your Circle CI user settings](https://app.circleci.com/settings/user/tokens) and choose "Personal API Tokens."
   2. Click on "Create New Token" and copy the newly generated token somewhere safe.
2. **Configuration**
   1. Go to [integrations catalog](https://app.envsecrets.com/integrations/catalog) in your envsecrets dashboard and choose "Circle CI."
   2. On the setup/connection page, enter your Circle CI personal access token you created above and save the configuration.

## Activation

1. Go to the [integrations](https://app.envsecrets.com/integrations) dashboard in your envsecrets organisation and under "Circle CI" choose "Manage."
2. Click on "Sync Secrets" button.
3. In the page that opens, select your envsecrets project, environment and your Circle CI organisation and project where you wish to push/sync your secrets.
4. Complete and save the form.

## Usage

1. Right after saving the configuration and activating an integration on a specific environment in envsecrets, your secrets will automatically get synced for the first time to your Circle CI project. It is advisable you open your Circle CI dashboard and check the values in your new secret.
2. From here on, everytime you create a new version of your secrets in your environment, the new values will automatically get pushed to your Circle CI project.
