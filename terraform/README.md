# Cloudflare Infrastructure

This folder manage Node.js Cloudflare settings using Terraform

### Contributing

To modify the Cloudflare settings, you must fork/clone this repository and submit a pull request with the changes. Any alterations made in the `main` branch will be deployed to the Cloudflare account automatically. So, the pull request is required to review the changes before they are deployed.

### Historical Context

Today, we use Terraform to manage DNS records in Cloudflare. Previously, we used the Cloudflare UI for this task. To begin using Terraform, we cloned the Cloudflare settings and migrated them as the initial Terraform state using the utility cf-terraforming. This step was completed only once, and the state was stored in Terraform Cloud.

Since the imported resources had non-human friendly names like "terraform_managed_resource_*," we cannot change their names to prevent recreation or updates of the resources. However, we can use our own naming conventions for new Terraform resources, and there is no need to run the cf-terraforming utility again.


### How to review changes in a PR?

The terraform plan is generated automatically in the PR. You can review the changes in the `terraform plan` section in the PR.

There are two possible scenarios:
- No changes
- Changes required

When changes are required you can see the details in the `terraform plan` section. Here you have several isolated examples of the changes:
- [Add resource](https://github.com/UlisesGascon/poc-nodejs-cloudflare-terraform/pull/5)
- [Update resource](https://github.com/UlisesGascon/poc-nodejs-cloudflare-terraform/pull/6)
- [Delete resource](https://github.com/UlisesGascon/poc-nodejs-cloudflare-terraform/pull/4)

Note that any change can combine several of the previous examples. For example, you can see a change that add a resource and update another one.

Once the PR is merged, the changes will be applied in the Cloudflare account via Github Action.

### Local development

#### IMPORTANT ⚠️
If you apply any plan in you local machine, you can trigger changes in the Cloudflare account. So, you must be careful with the changes you are applying in your local environment. In order to review/create changes you are not require to do local development as the github pipeline will generate a plan with the changes.


#### Requirements
- Terraform version `Terraform v1.4.5` used to build this infrastructure. [How to install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- You will need a `TF_API_TOKEN` in you environment with a valid Terraform cloud API Key. [How to create a Terraform cloud API Key](https://www.terraform.io/docs/cloud/users-teams-organizations/api-tokens.html#creating-an-api-token)


### Reference
- [Fireship | Terraform in 100 Seconds](https://www.youtube.com/watch?v=tomUWcQ0P3k)
- [Terraform Cheatsheet](https://acloudguru.com/blog/engineering/the-ultimate-terraform-cheatsheet)
- [Youtube | Automate Cloudflare with Terraform and GitHub Actions! - Terraform Tutorial for Beginners](https://www.youtube.com/watch?v=FmYvrxYvBP0)
- [Techno Tim Docs | Automate Cloudflare with Terraform and GitHub Actions! - Terraform Tutorial for Beginners](https://docs.technotim.live/posts/terraform-cloudflare-github/)