---
name: nextjs-turbopack
description: Next.js 16+ and Turbopack — incremental bundling, FS caching, dev speed, and when to use Turbopack vs webpack.
license: MIT
---

# Next.js and Turbopack

Next.js 16+ uses Turbopack by default for both local development and production builds. It is an incremental bundler written in Rust.

## When to Use

- **Turbopack (default dev)**: Use for day-to-day development. Faster cold start and HMR, especially in large apps.
- **Webpack fallback**: If you need webpack compatibility, use `next dev --webpack` or `next build --webpack`.
- **Production**: In Next.js 16+, `next build` uses Turbopack by default; `--webpack` explicitly opts out.

Use when: developing or debugging Next.js 16+ apps, diagnosing slow dev startup or HMR, or optimizing production bundles.

## How It Works

- **Turbopack**: Incremental bundler for Next.js development and production builds.
- **Default bundler**: From Next.js 16, both `next dev` and `next build` use Turbopack by default.
- **File-system caching**: In Next.js 16.0, development caching is beta and requires `experimental.turbopackFileSystemCacheForDev: true`. From 16.1, development caching is stable and enabled by default. These version boundaries concern development caching, not build caching.
- **Bundle Analyzer (Next.js 16.1+)**: Run `next experimental-analyze` to inspect bundles and find heavy dependencies. This command does not produce an application build.

## Examples

### Commands

```bash
next dev
next build
next start
```

### Usage

Run `next dev` for local development with Turbopack. Use the Bundle Analyzer (see Next.js docs) to optimize code-splitting and trim large dependencies. Prefer App Router and server components where possible.

## Best Practices

- Stay on a recent Next.js 16.x for stable Turbopack and caching behavior.
- If dev is slow, ensure you're on Turbopack (default) and that the cache isn't being cleared unnecessarily.
- For production bundle size issues, use the official Next.js bundle analysis tooling for your version.

References: [Next.js 16](https://nextjs.org/blog/next-16), [Next.js 16.1](https://nextjs.org/blog/next-16-1), [Next.js CLI](https://nextjs.org/docs/app/api-reference/cli/next).
