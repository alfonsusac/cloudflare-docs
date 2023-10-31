---
pcx_content_type: concept
title: Git integration
---

# Git integration

Cloudflare supports connecting Cloudflare Pages to your GitHub and GitLab repositories to look for new changes to your project.

## Custom branches

Suppose you have a custom Git workflow that uses specific branches to represent your project's production build. In that case, you can specify a custom branch when creating (or managing an existing) project in the Pages dashboard by going to  **Settings** > **Builds & deployments** and clicking the **Configure Production deployments** button. You can change the production branch to any other branch in the dropdown menu under **production branch**.

You can also use [preview deployments](/pages/platform/preview-deployments/) to preview how the new version of your project looks before merging into `production`. In addition, Pages allows you to configure which of your preview branches are built and deployed by using [branch build controls](/pages/platform/branch-build-controls/).

To configure this in your Pages project go to **Settings** > **Builds & deployments** > **Configure preview deployment** and select **Custom branches**. Here you can specify branches you wish to include and exclude from automatic deployments in the provided configuration fields. To learn more refer to the [branch build controls](/pages/platform/branch-build-controls/) documentation.


## Organizational access

You can deploy projects to Cloudflare Pages from your open-source team, company, or side project on both GitHub and GitLab.

### GitHub

When authorizing Cloudflare Pages to access a GitHub account, you can specify access to your individual account or an organization that you belong to on GitHub. In order to be able to add the Cloudflare Pages installation to that organization, your user account must be an owner or have the appropriate role within the organization (i.e. the Github Apps Manager role). More information on these roles can be seen on [Github's documentation](https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization#github-app-managers).

### GitLab

By authorizing Cloudflare Pages to access your GitLab account, you will automatically allow access to organizations, groups, and namespaces your GitLab account can access for use by Cloudflare Pages. Managing access to these organizations and groups is handled by Gitlab.

## Removing access to your GitHub account

You can remove Cloudflare Pages' access to your GitHub account by viewing the [**Applications** page](https://github.com/settings/installations) on GitHub. Note that removing access to GitHub will also disable new builds, though the last build of your site will continue to be hosted via Cloudflare Pages.

## Removing access to your GitLab account

You can remove Cloudflare Pages' access to your GitLab account by navigating to **User Settings** > **Applications** > **Authorized Applications**. Find the applications called Cloudflare Pages and select the **Revoke** button to revoke access.

## Pausing Automatic Builds

By default, Cloudflare Pages automatically builds and deploys a project whenever its repository receives new commits. You can pause this behavior to keep your website at a particular version and manually deploy new versions when desired.

To pause automatic deployments, go to the Pages project's **Settings** > **Builds & deployments** > select **Pause deployments** at the end of the page.

![Pausing a deployment in the Settings of your Pages project](/images/pages/platform/git.pause.png)

Selecting **Pause deployments** will present a confirmation and, once confirmed, the **Pause deployments** button will be replaced with a **Resume deployments** button. While paused, your **Deployments** list will present a banner message, reminding you that automatic deployments are not enabled.

## Reinstalling a git installation

When encountering Git integration related issues, one potential troubleshooting step is attempting to uninstall and reinstall an installation. The process for each git provider is provided below

### Github

1. Go to the installation settings page on Github
    1. `https://github.com/settings/installations` for individual accounts
    1. `https://github.com/organizations/[YOUR_ORGANIZATION_NAME]/settings/installations` for organizational accounts
2. If the Cloudflare Pages installation is there, click `Configure`, and click `Uninstall 'Cloudflare Pages'` (if there is no "Cloudflare Pages" installation, the user doesn't need to do anything)
3. Go back to the `Workers & Pages` overview page at `https://dash.cloudflare.com/[YOUR\_ACCOUNT\_ID]/workers-and-pages`. Click `Create application` > `Pages` > `Connect to git`
4. Click the '+ Add account' button, click the Github account you want to add, and then click `Install & Authorize`.
5. You should be redirected to the create project page with your Github account or organization in the account list.
6. Attempt to make a new deployment with your project which was previously broken.

### Gitlab

1. Go to your application settings page on Gitlab located here: https://gitlab.com/-/profile/applications
2. Click the "Revoke" button on your Cloudflare Pages installation if it exists.
3. Go back to the `Workers & Pages` overview page at `https://dash.cloudflare.com/[YOUR\_ACCOUNT\_ID]/workers-and-pages`. Click `Create application` > `Pages` > `Connect to git`
4. Select the gitlab tab at the top, click the '+ Add account' button, click the Gitlab account you want to add, and then click `Authorize` on the modal titled "Authorize Cloudflare Pages to use your account? ".
5. You should be redirected to the create project page with your Github account or organization in the account list.
6. Attempt to make a new deployment with your project which was previously broken.

## Troubleshooting

If you run into any issues related to deployments failing, check your project dashboard to see if there are any SCM installation warnings listed. To resolve any errors displayed in the Cloudflare Pages dashboard, follow the steps listed below.

### `The Cloudflare Pages installation was uninstalled on GitHub. To reinstall, log in to the Cloudflare dashboard > Workers & Pages > Create an application > Connect to git > + Add account.`

To resolve this issue, please follow the steps provided above in the [Reinstalling a git installation section](/pages/platform/git-integration/#reinstalling-a-git-installation) for the applicable SCM provider. If the issue persists even after uninstalling and reinstalling, please contact support.

### `Cloudflare Pages is not properly installed on your git account. Please uninstall and reinstall your git installation to make new deployments.`

To resolve this issue, please follow the steps provided above in the [Reinstalling a git installation section](/pages/platform/git-integration/#reinstalling-a-git-installation) for the applicable SCM provider. If the issue persists even after uninstalling and reinstalling, please contact support.

### `The Cloudflare Pages installation has been suspended. Please unsuspend in your GitHub installation settings.`

Go to your Github installation settings located at:

* `https://github.com/settings/installations` for individual accounts
* `https://github.com/organizations/[YOUR_ORGANIZATION_NAME]/settings/installations` for organizational accounts

Click "Configure" on the Cloudflare Pages application. Scroll down to the bottom of the page and click "Unsuspend" to allow Cloudflare Pages to make future deployments.

### `You have no linked repositories matching the provided name. Please verify this repository exists on the correct git account.`

You may have deleted or transferred the repository associated with this Cloudflare Pages project. For a deleted repository, you will need to create a new Cloudflare Pages project with a repository that has not been deleted. For a transferred repository, you can either transfer the repository back to the original Git account or you will need to create a new Cloudflare Pages project with the transferred repository.

### `This repo is unable to be accessed. Please review your GitHub repo access permissions for the Cloudflare Pages installation to make new deployments.`

You may have excluded this repository from your installation's repository access settings.  Go to your Github installation settings located at:

* `https://github.com/settings/installations` for individual accounts
* `https://github.com/organizations/[YOUR_ORGANIZATION_NAME]/settings/installations` for organizational accounts

Click "Configure" on the Cloudflare Pages application. Under "Repository access," ensure that the repository associated with your Cloudflare Pages project is included in the list.

### `There is an issue with your Cloudflare Pages git installation. Please contact support.`

This is an internal error in the Cloudflare Pages SCM system. You can attempt to [reinstalling your git installation](/pages/platform/git-integration/#reinstalling-a-git-installation), but if the issue persists please contact support.