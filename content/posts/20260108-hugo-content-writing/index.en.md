---
title: "Building a Hugo Blog (4): Content Writing and Markdown Shortcodes"
slug: "hugo-content-writing"
date: 2026-01-08T20:30:00+09:00
description: "Learn how to efficiently manage images using Hugo's Page Bundle method and enrich your posts using the powerful shortcodes (Alert, Badge, etc.) provided by the Blowfish theme."
series: ["Building a Hugo Blog"]
series_order: 4
categories: ["Writing", "Guide"]
tags: ["Markdown", "Front Matter", "Content"]
draft: false
# Thumbnail : https://pixabay.com/photos/typing-apple-computer-computer-desk-4156011/
---

In the previous posts, we built the framework of our blog and gave it a polished look. Now, it’s time to fill this beautiful house with furniture—specifically, **Content**.

Hugo builds content based on the Markdown format. While it might feel unfamiliar at first for those used to WYSIWYG editors like WordPress or Medium, there is no better environment for a developer who handles both code and text simultaneously.

Today, we will explore Hugo's content creation rules and the **Shortcodes** feature of the Blowfish theme, which helps make your posts more engaging.

---

## 1. Creating a New Post

While you can create files directly in your file explorer, using Hugo commands automatically generates a file with the current date and basic template.

Navigate to your project root in the terminal and try the following command:

```powershell
# hugo new content posts/[post-name]/index.md
hugo new content posts/hello-world/index.md
```

Hugo's default process is to read the `index.md` file within a folder. You can write your primary language content in `index.md`, and for other languages, you can create files like `index.en.md`.

```Markdown
.
├── content
│   └── posts
│       └── hello-world
│           ├── index.en.md
│           └── index.md
·
```

Technically, you can just create a single file like `hello-world.md` directly inside the posts folder. However, managing images becomes difficult this way. Creating a dedicated folder for each post (Page Bundle) is the best method for long-term maintenance.

---

## 2. Front Matter Configuration

Open the generated `index.md` file, and you will see a section at the top wrapped in `--- (or +++)`. This is called `Front Matter`, and it contains the metadata for your post.

```Markdown
---
title: 'Hello World!'
date: 2026-01-08T20:30:00+09:00
categories: ["Blog"]
tags: ["Hugo", "Content"]
draft: true
---
```

- **title**: Sets the title of the post.
- **date**: Sets the creation date. Since Korea is 9 hours ahead of UTC, add `+09:00` after the time.
- **categories/tags**: Used for classification. You can add multiple values in an array format `["A", "B"]`.
- **draft**: Indicates if the post is a draft. Change this to `false` when you are ready to publish.

---

## 3. Inserting Images

I recommend creating an `img/` folder within each post folder and placing your image files there.

```Markdown
.
├── content
│   └── posts
│       └── hello-world
│           ├── img
│           │   └── universe.jpg
│           ├── index.en.md
│           └── index.md
·
```

For example, copy an image (e.g., universe.jpg) into the img folder of your hello-world post. Then, you can insert it into the body text like this:

**Syntax:**

```Markdown
<!--content/posts/hello-world/img/universe.jpg -->

<!--Example 1:-->
![Space Photo](img/universe.jpg)

<!--Example 2:-->
![Space Photo](img/universe.jpg "Image [by Gerd Altmann](https://pixabay.com/users/geralt-9301/) from [Pixabay](https://pixabay.com/illustrations/universe-sky-stars-space-cosmos-2742113/)")
```

**Result with caption:**

![Space Photography](img/universe.jpg "Image [by Gerd Altmann](https://pixabay.com/users/geralt-9301/) from [Pixabay](https://pixabay.com/illustrations/universe-sky-stars-space-cosmos-2742113/)")

---

## 4. Utilizing Shortcodes

Standard Markdown (bold, lists, links, etc.) is often sufficient, but if you want more dynamic elements, Shortcodes are the way to go.

You can find more varieties in the [Blowfish Shortcodes Official Documentation](https://blowfish.page/docs/shortcodes/).

### ① Alert (Notice Boxes)

Used to highlight important information or tips.

**Syntax:**

```Markdown
{{</* alert "twitter" */>}}
**Warning!** This action is destructive!
{{</* /alert */>}}
```

**Result:**

{{< alert "twitter" >}} This is a Twitter-style alert box. {{< /alert >}}

**Types**: Various types like `warning`(yellow), `neutral`(gray), and `info`(blue) are supported.

### ② Badge

Allows you to add small tags within the text.

**Syntax:**

```Markdown
{{</* badge */>}}New Badge{{</* /badge */>}}
```

**Result:**

{{< badge >}}New Badge{{< /badge >}}

### ③ Embedding YouTube Videos

You can easily embed videos using just the YouTube video ID.

**Syntax:**

```Markdown
{{</* youtubeLite id="pNi9PjmbUrI" label="HANRORO_Let Me Love My Youth" */>}}
```

**Result:**

{{< youtubeLite id="pNi9PjmbUrI" label="HANROROLet Me Love My Youth" >}}

### ④ Code Blocks (Syntax Highlighting)

The core of any dev blog. Specifying the language will apply syntax highlighting. This is the shortcode I use most frequently.

**Syntax:**

````Plaintext
```python
def hello():
  print("Hello Hugo!")
```
````

**Result:**

```python
def hello():
  print("Hello Hugo!")
```

---

## 5. Live Preview

If you keep `hugo server` running in your terminal while writing or editing, the site will automatically refresh and show the results every time you save your file (`Ctrl + S`).

{{< alert >}} Note 1: If your post doesn't appear after running `hugo server`, it’s likely because the `draft` value in the Front Matter is set to `true`. To view draft posts, run the server with the `hugo server -D` command, or simply change `draft` to `false`. {{< /alert >}}

</br>

{{< alert icon="fire" cardColor="#db2f3dff" iconColor="#ffffff" textColor="#ffffff" >}} Note 2: If the post creation time is set to a future time relative to the build date, the post may not be visible. You can set the time to the past or configure `buildFuture = true` in your `config/_default/hugo.toml` file. {{< /alert >}}

---

## 6. Closing

You have now learned how to write and style your content. You should see your blog coming together nicely on `localhost:1313`.

I will continue to introduce more ways to customize your blog in future posts.

In the next part, I will show you **how to deploy your blog** so that others can access it.
