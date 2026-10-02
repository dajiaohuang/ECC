---
name: nextjs-turbopack
description: Next.js 16+ 和 Turbopack — 增量打包、文件系统缓存、开发速度，以及何时使用 Turbopack 与 webpack。
origin: ECC
---

# Next.js 与 Turbopack

Next.js 16+ 在本地开发和生产构建中均默认使用 Turbopack。它是用 Rust 编写的增量捆绑器。

## 何时使用

* **Turbopack (默认开发模式)**：用于日常开发。冷启动和热模块替换速度更快，尤其是在大型应用中。
* **切换到 webpack**：需要 webpack 兼容性时，使用 `next dev --webpack` 或 `next build --webpack`。
* **生产环境**：Next.js 16+ 的 `next build` 默认使用 Turbopack；使用 `--webpack` 可切换到 webpack。

适用场景：开发或调试 Next.js 16+ 应用，诊断开发启动或热模块替换速度慢的问题，或优化生产环境捆绑包。

## 工作原理

* **Turbopack**：用于 Next.js 开发和生产构建的增量捆绑器。
* **默认捆绑器**：从 Next.js 16 开始，`next dev` 和 `next build` 均默认使用 Turbopack。
* **文件系统缓存**：Next.js 16.0 的开发缓存处于测试阶段，需要设置 `experimental.turbopackFileSystemCacheForDev: true`。从 16.1 开始，开发缓存稳定且默认启用。这些版本条件针对开发缓存，不代表生产构建缓存的启用条件。
* **捆绑包分析器 (Next.js 16.1+)**：运行 `next experimental-analyze` 检查捆绑包和大型依赖。该命令不会生成应用构建。

## 示例

### 命令

```bash
next dev
next build
next start
```

### 使用

运行 `next dev` 以使用 Turbopack 进行本地开发。使用捆绑包分析器（参见 Next.js 文档）来优化代码分割并剔除大型依赖。尽可能优先使用 App Router 和服务器组件。

## 最佳实践

* 保持使用较新的 Next.js 16.x 版本，以获得稳定的 Turbopack 和缓存行为。
* 如果开发速度慢，请确保你正在使用 Turbopack（默认），并且缓存没有被不必要地清除。
* 对于生产环境捆绑包大小问题，请使用你所用版本的官方 Next.js 捆绑包分析工具。

References: [Next.js 16](https://nextjs.org/blog/next-16), [Next.js 16.1](https://nextjs.org/blog/next-16-1), [Next.js CLI](https://nextjs.org/docs/app/api-reference/cli/next).
