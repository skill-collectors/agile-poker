---
layout: page
title: Manual deploys
permalink: /how-to/deploy-manually
---

This describes how you could manually deploy the app from your workstation.

Generally, you will not need to do this. You can run the frontend with `vite` and the backend with `localstack` without actually deploying anything (or even having an internet connection). Remember also that the app will be deployed to QA whenever a PR is built, and it will be deployed to production whenever a PR is merged into `main`.

However, you might want to do this if you want to deploy your own copy of the app into your own AWS account. It would also allow you to test something in AWS that localstack doesn't support or do experimental work without changing the shared QA environment.

## Prerequisites

- Update the `apexDomain` in `infra/index.ts` to specify a domain that you already own and have set up in Route53.
    - Ideally the domain should be more externalized. This is a good opportunity to improve the codebase. Consider [creating a task](https://github.com/skill-collectors/agile-poker/issues/new?assignees=&labels=&template=new-task.md&title=Externalize%20domain) on the project board and giving it a try.
- Ensure that your AWS CLI account has the correct deploy permissions. The following policies are sufficient, but could probably be narrower:
    - `AmazonS3FullAccess`
    - `CloudFrontFullAccess`
    - `AmazonRoute53FullAccess`
    - `AWSCertificateManagerFullAccess`

## Deploying

From the project root, run

```sh
./deploy-dev.sh
```

This will:

1. Run `pulumi up` for the `dev` stack
2. Build the frontend
3. Sync the frontend build output to the app's S3 bucket
4. Invalidate the CloudFront cache
