---
title: "Cloudflare Pages: How to Fix Hugo Blog Build Fail (can't evaluate field Locale)"
slug: cloudflare-pages-hugo-build-failed-locale
date: 2026-05-21T12:00:00+09:00
description: "Analyze the cause of the Hugo build error that occurs after applying the latest Blowfish theme on Cloudflare Pages, and learn how to resolve the deployment failure by setting the HUGO_VERSION environment variable."
summary: "A step-by-step guide to resolving the Hugo build failure on Cloudflare Pages due to the 'can't evaluate field Locale' error after updating the Blowfish theme by forcing a higher Hugo version using environment variables."
categories: ["Hugo", "Web Development", "Cloudflare"]
tags: ["Hugo", "Blowfish", "Cloudflare Pages", "Build Error", "Deployment", "Environment Variable"]
draft: false
---

After updating my multilingual settings to comply with the latest Blowfish theme specifications, I pushed the changes to GitHub.

Since I had verified that everything ran perfectly on my local environment (`hugo server`) without any warnings, I naturally expected the deployment to succeed. However, the build failed on **Cloudflare Pages** with an `exit code 1`.

In this post, I will share the cause of this issue analyzed from the logs and the simplest way to fix it.

---

## 1. The Issue: Cloudflare Build Log Error

Checking the deployment failure logs in the Cloudflare dashboard revealed the following error messages:

{{< figure src="img/01-cloudflare-build-error-en.png" alt="Cloudflare Pages build log screen showing deployment failed due to can't evaluate field Locale error" >}}

```
2026-05-20T08:23:35.40313Z     WARN  Module "blowfish" is not compatible with this Hugo version: 0.158.0/0.161.1 extended; run "hugo mod graph" for more information.
...
2026-05-20T08:23:35.558814Z    ERROR render of "/404" failed: ... can't evaluate field Locale in type *langs.Language
...
2026-05-20T08:23:35.564486Z    Failed: Error while executing user command. Exited with error code: 1
```

Analyzing the logs made the cause very clear:

- **Theme Requirements**: The updated Blowfish theme internally requires `Hugo 0.158.0` or `0.161.1 or higher`.

- **Cloudflare's Current Environment**: The default build system in Cloudflare Pages was using Hugo version `v0.147.7`.

While my local machine was running the latest Hugo version and encountered no problems, the Cloudflare server's Hugo engine was too outdated to interpret the structure of the newer theme (such as `.Site.Language.Locale`), causing the build to crash.

---

## 2. Solution: Specifying the HUGO_VERSION Environment Variable

You can easily resolve this problem by setting an `Variable` that instructs Cloudflare Pages to use the latest version of Hugo when executing the build.

### ① Navigate to Cloudflare Project Settings

Log in to the [Cloudflare Dashboard](https://dash.cloudflare.com/ec5616c3d09ae19cb775579baf1ff640) and select your blog project. Click on the `Settings` tab in the top menu, then click `Variables and Secrets` in the left sidebar.

{{< figure src="img/02-cloudflare-settings-env-en.png" alt="Screenshot selecting the Environment variables tab in Cloudflare Pages project settings menu" >}}

### ② Add Variable

In the `Variables and secrets` section, click the **Add** button and input the following:

{{< figure src="img/03-cloudflare-add-variable-en.png" alt="Screenshot entering HUGO_VERSION as variable name and 0.161.1 as value in Cloudflare environment variable settings" >}}

- **Variable name**: `HUGO_VERSION`

- **Value**: `0.161.1` (A stable Hugo version required by the theme)

Once entered, click the **Save** button at the bottom to apply the settings.

### ③ Verify the Configured Variable

You should see the added variable successfully applied, as shown below.

Since the changes only apply to subsequent deployments, you will need to trigger a redeployment.

{{< figure src="img/04-cloudflare-env-check-en.png" alt="Screenshot showing the variable successfully added and applied in Cloudflare" >}}

---

## 3. Triggering Redeployment

After saving the settings, go to the `Deployments` tab of the dashboard and click **Retry deployment**, or push an empty commit to GitHub to trigger the build process again.

{{< figure src="img/05-cloudflare-build-success-en.png" alt="Screenshot showing the Cloudflare Pages build completed successfully after applying the environment variable" >}}

Unlike before, the specified newer version of the Hugo engine will run, generating the static files without any errors and successfully completing the deployment.

---

## Conclusion

When deploying to environments like GitHub Pages or Cloudflare Pages, build failures due to mismatches between local and server engine versions are quite common.

Particularly when upgrading rapidly evolving themes like Blowfish, it is a good habit to check the minimum Hugo version required by the theme and synchronize it with your Cloudflare environment variables.

I hope this guide helps anyone who was frustrated by this deployment failure, as I was.
