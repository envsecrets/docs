---
description: >-
  Setup and usage guide on how to continuously sync your secrets with Github
  Actions.
---

# Github Actions

### About Github Secrets

Secrets are encrypted variables that you create in an organization, repository, or repository environment. The secrets that you create are available to use in GitHub Actions workflows.&#x20;

For secrets stored at the organization-level, you can use access policies to control which repositories can use organization secrets. Organization-level secrets let you share secrets between multiple repositories, which reduces the need for creating duplicate secrets. Updating an organization secret in one location also ensures that the change takes effect in all repository workflows that use that secret.

For secrets stored at the environment level, you can enable required reviewers to control access to the secrets. A workflow job cannot access environment secrets until approval is granted by required approvers.

#### [Naming your secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#naming-your-secrets) <a href="#naming-your-secrets" id="naming-your-secrets"></a>

The following rules apply to secret names:

* Names can only contain alphanumeric characters (`[a-z]`, `[A-Z]`, `[0-9]`) or underscores (`_`). Spaces are not allowed.
* Names must not start with the `GITHUB_` prefix.
* Names must not start with a number.
* Names are not case-sensitive.
*   Names must be unique at the level they are created at.

    For example, a secret created at the environment level must have a unique name in that environment, a secret created at the repository level must have a unique name in that repository, and a secret created at the organization level must have a unique name at that level.

    If a secret with the same name exists at multiple levels, the secret at the lowest level takes precedence. For example, if an organization-level secret has the same name as a repository-level secret, then the repository-level secret takes precedence. Similarly, if an organization, repository, and environment all have a secret with the same name, the environment-level secret takes precedence.

To help ensure that GitHub redacts your secret in logs, avoid using structured data as the values of secrets. For example, avoid creating secrets that contain JSON or encoded Git blobs.

#### [Accessing your secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#accessing-your-secrets) <a href="#accessing-your-secrets" id="accessing-your-secrets"></a>

To make a secret available to an action, you must set the secret as an input or environment variable in the workflow file. Review the action's README file to learn about which inputs and environment variables the action expects. For more information, see "[Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob\_idstepsenv)."

You can use and read encrypted secrets in a workflow file if you have access to edit the file. For more information, see "[Access permissions on GitHub](https://docs.github.com/en/get-started/learning-about-github/access-permissions-on-github)."

**Warning:** GitHub automatically redacts secrets printed to the log, but you should avoid printing secrets to the log intentionally.

Organization and repository secrets are read when a workflow run is queued, and environment secrets are read when a job referencing the environment starts.

You can also manage secrets using the REST API. For more information, see "[Actions](https://docs.github.com/en/rest/actions#secrets)."
