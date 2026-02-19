---
title: "What I Learned Building This Site with Astro"
description: "A quick tour of Astro 5's content collections, static rendering, and why it's perfect for personal sites."
pubDate: 2025-11-15
tags: ["astro", "web dev", "tutorial"]
draft: false
---

After spending a weekend building this site, I have thoughts. Astro is genuinely delightful — and it took me an embarrassingly short time to understand why people love it.

## What is Astro, exactly?

Astro is a web framework built for content-heavy sites. Its key idea is **zero JavaScript by default** — pages are rendered to HTML at build time, and interactivity is opt-in. This makes for very fast sites without much effort.

## Content Collections

The feature I used most is [Content Collections](https://docs.astro.build/en/guides/content-collections/). You define a schema with Zod, put your Markdown files in `src/content/`, and Astro gives you type-safe access to all your content.

```typescript
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  schema: z.object({
    title: z.string(),
    pubDate: z.coerce.date(),
    tags: z.array(z.string()).default([]),
  }),
});

export const collections = { blog };
```

Then in any page:

```typescript
import { getCollection } from 'astro:content';
const posts = await getCollection('blog');
```

That's it. Type-safe, fast, simple.

## Scoped Styles

Every `.astro` file can have a `<style>` block that's automatically scoped to that component. No class name collisions, no CSS modules boilerplate. It just works.

## Final Verdict

If you want a fast personal site with a blog, Astro is the move. The learning curve is gentle, the DX is great, and the output is genuinely fast.

10/10, would build again.
