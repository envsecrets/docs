---
description: >-
  Setup and usage guide on how to continuously sync your secrets with AWS
  Secrets Manager.
---

# AWS Secrets Manager

## Prerequisites

* AWS Console Access
* AWS IAM access
  * Ability to create IAM roles and Policies
  * Ability to access IAM users

## Setup

1.  **Create new AWS policy**

    1. Navigate to the [Create New Policy](https://console.aws.amazon.com/iam/home#/policies$new?step=edit) section in the AWS IAM console.
    2. Switch to the JSON tab.
    3. Enter the following policy.

    ```
    ```

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "AllowSecretsManagerAccess",
                "Effect": "Allow",
                "Action": [
                    "secretsmanager:GetSecretValue",
                    "secretsmanager:DescribeSecret",
                    "secretsmanager:PutSecretValue",
                    "secretsmanager:CreateSecret",
                    "secretsmanager:DeleteSecret",
                    "secretsmanager:TagResource",
                    "secretsmanager:UpdateSecret"
                ],
                "Resource": "*"
            }
        ]
    }
    ```

    4. Optionally provide tags.
    5. Name your policy as "envsecrets" and hit create.


2.  **Create an AWS Role**

    1. Navigate to the [create role](https://console.aws.amazon.com/iamv2/home#/roles/create?step=selectEntities) section of the AWS IAM console
    2. Select **AWS account** for the **Trusted entity type**
    3. Select **Another AWS account** under **An AWS account**
       1. Enter **284838358097** for the **Account ID**. This is envsecrets's account ID.
    4. Under **Options** check **Require external ID**
       1. Enter your organisation ID for the External ID. You can obtain your organisation ID by visiting the [organisation settings](https://app.envsecrets.com/settings) in your envsecrets dashboard.
       2. Leave **require MFA** unchecked
    5. Attach the "envsecrets" policy you created above.
    6. Name your role as "envsecrets" and complete the role setup.
    7. Copy the new role's ARN.


3. **Configuration**
   1. Go to [integrations catalog](https://app.envsecrets.com/integrations/catalog) in your envsecrets dashboard and choose "AWS Secrets Manager."
   2. On the setup/connection page, enter your AWS region and ARN of the "envsecrets" role you created above and save.

## Activation

1. Go to the [integrations](https://app.envsecrets.com/integrations) dashboard in your envsecrets organisation and under "AWS Secrets Manager" choose "Manage."
2. Click on "Sync Secrets" button.
3. In the page that opens, select your envsecrets project, environment and enter the name with which you wish you save your secret in AWS Secrets Manager.
4. Complete and save the form.

## Usage

1. Right after saving the configuration and activating an integration on a specific environment in envsecrets, your secrets will automatically get synced for the first time to your AWS Secrets Manager. It is advisable you open your ASM dashboard and check the values in your new secret.
2. From here on, every time you create a new version of your secrets in your environment, the new values will automatically get pushed to your ASM secret.

{% hint style="warning" %}
Every new version of your secret in envsecrets will create a new version of the existing secret in AWS Secrets Manager.
{% endhint %}
