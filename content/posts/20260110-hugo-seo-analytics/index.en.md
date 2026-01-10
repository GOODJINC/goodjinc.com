---
title: "Building a Hugo Blog (6): Search Engine Registration and Google Analytics"
slug: hugo-seo-analytics
date: 2026-01-10T10:50:00+09:00
description: "The final step to making your blog known to the world! We'll cover how to register with Google and Naver search engines and how to connect Google Analytics 4 (GA4)."
series: ["Building a Hugo Blog"]
series_order: 6
categories: ["SEO", "Operation"]
tags:
  [
    "Search Engine",
    "Google Search Console",
    "Naver Search Advisor",
    "Google Analytics",
    "GA4",
    "SEO",
  ]
draft: false
# Thumbnail : https://pixabay.com/photos/digital-marketing-technology-1433427/
---

We have finally reached the grand finale! After following the first five parts, you’ve successfully built and deployed your blog. However, at this stage, it’s like a beautiful island that no one knows how to visit.

Today, we will cover **Search Engine Registration**—clearing a path so search engines can find and index your posts—and **Google Analytics 4 (GA4)**, which allows you to analyze who is visiting your blog and how they interact with your content.

{{< alert >}}
Please note that search engine registration and Google Analytics do not reflect data immediately. It may take several days for crawling, indexing, and data stabilization to occur.
{{< /alert >}}

---

## 1. Preparation: Verify Your Sitemap

Before registering with search engines, you need a "map" that helps search robots understand the structure of your site. Hugo automatically generates a `sitemap.xml` file when it builds your site.

- **How to check**: Add `/sitemap.xml` to the end of your deployed URL.
- **Example**: `https://yourdomain.com/sitemap.xml`

---

## 2. Registering with Naver Search Advisor

If you are targeting the Korean market, this is a mandatory step. Since Naver is a major search platform in Korea, ensure your blog is registered here.

1. Log in to [Naver Search Advisor](https://searchadvisor.naver.com/).
2. Go to the **Webmaster Tools** and register your blog URL.
3. **Site Ownership Verification**: Download the HTML verification file provided by Naver.
4. **Upload File**: Place the downloaded file into your project's **`static/`** folder. (Files in this folder are moved to the root directory upon deployment.)
5. Run `git push` to deploy the change, then click the **[Verify]** button on the Naver site.
6. **Submit Sitemap**: Go to [Site Management] > [Requests] > [RSS Submission] and enter `index.xml`. Then, go to [Sitemap Submission] and enter `sitemap.xml`.

> [!TIP]
> Here are the typical URL formats for a Hugo (Blowfish theme) blog:  
> **RSS**: `https://yourdomain.com/index.xml`  
> **Sitemap**: `https://yourdomain.com/sitemap.xml`

---

## 3. Registering with Google Search Console

This is the most critical step for appearing in Google search results globally.

1.  Visit the [Google Search Console](https://search.google.com/search-console/).
2.  Select the **URL Prefix** method and enter your blog's address.
3.  **Ownership Verification**: Download the provided HTML file, place it in your **`static/`** folder, and deploy it via `git push`.
4.  **Submit Sitemaps**: Navigate to the [Sitemaps] menu on the left sidebar, type `sitemap.xml`, and click [Submit].

> [!TIP]
> Besides HTML file upload, Google Search Console offers various other verification methods, such as using Google Analytics or DNS records via Cloudflare.

---

## 4. Connecting Google Analytics 4 (GA4)

To understand who is reading your posts and where they are coming from, you need a data analysis tool. The Blowfish theme makes it incredibly easy to integrate Google Analytics.

### ① Get Your GA4 Measurement ID

1.  Create an account and property at [Google Analytics](https://analytics.google.com/).
2.  In the Data Stream settings, select 'Web' and enter your blog's URL.
3.  Copy the generated **'Measurement ID'** (format: `G-XXXXXXXXXX`).

### ② Apply the ID to the Blowfish Theme

Open the `config/_default/hugo.toml` file in your project root and enter your Measurement ID in the `googleAnalytics` field.

```toml
# config/_default/hugo.toml

googleAnalytics = "G-XXXXXXXXXX"
```

With just this single line of configuration, the analysis script will be automatically injected into your blog.

---

## 5. Conclusion: Believe in the Power of Recording

The "Building a Hugo Blog" series has finally come to an end!

We’ve covered everything from setting up the environment on Windows to customizing, writing content, and finally deploying and optimizing for SEO.

All that’s left now is to fill this space with your valuable experiences and knowledge, one post at a time.

Recording your thoughts is a powerful habit. I hope this series has been a helpful guide for your new beginning.

Thank you for reading! 😊
