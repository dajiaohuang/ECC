---
name: nextjs-turbopack
description: Next.js 16+とTurbopack — インクリメンタルバンドリング、FSキャッシング、開発速度、Turbopackとwebpackをいつどちらかどうかを選ぶか。
origin: ECC
---

# Next.jsとTurbopack

Next.js 16+はローカル開発と本番ビルドの両方でデフォルトでTurbopackを使用する。Rustで書かれたインクリメンタルバンドラーである。

## 使用するタイミング

- **Turbopack（デフォルト開発）**: 日々の開発に使用する。特に大規模アプリでコールドスタートとHMRが速い。
- **Webpackへの切り替え**: webpackとの互換性が必要な場合は`next dev --webpack`または`next build --webpack`を使用する。
- **プロダクション**: Next.js 16+の`next build`はデフォルトでTurbopackを使用する。`--webpack`でwebpackに切り替える。

使用するケース: Next.js 16+アプリの開発またはデバッグ、開発起動やHMRの遅延を診断するとき、またはプロダクションバンドルを最適化するとき。

## 仕組み

- **Turbopack**: Next.jsの開発と本番ビルド用インクリメンタルバンドラー。
- **デフォルトバンドラー**: Next.js 16から、`next dev`と`next build`の両方がデフォルトでTurbopackを使用する。
- **ファイルシステムキャッシング**: Next.js 16.0の開発キャッシュはベータ版で、`experimental.turbopackFileSystemCacheForDev: true`が必要。16.1からは開発キャッシュが安定版になり、デフォルトで有効。これらのバージョン条件は開発キャッシュに関するもので、本番ビルドのキャッシュには適用しない。
- **バンドルアナライザー（Next.js 16.1+）**: `next experimental-analyze`でバンドルと重い依存関係を検査する。このコマンドはアプリケーションのビルドを生成しない。

## 例

### コマンド

```bash
next dev
next build
next start
```

### 使用方法

ローカル開発にはTurbopackで`next dev`を実行する。バンドルアナライザー（Next.jsドキュメント参照）を使用してコード分割を最適化し、大きな依存関係を削減する。可能な限りApp RouterとサーバーコンポーネントをBestPracticeとして使用する。

## ベストプラクティス

- 安定したTurbopackとキャッシングの動作のために最新のNext.js 16.xを使い続ける。
- 開発が遅い場合は、Turbopack（デフォルト）を使用していることと、キャッシュが不必要にクリアされていないことを確認する。
- プロダクションバンドルサイズの問題には、使用中のバージョンの公式Next.jsバンドル解析ツールを使用する。

References: [Next.js 16](https://nextjs.org/blog/next-16), [Next.js 16.1](https://nextjs.org/blog/next-16-1), [Next.js CLI](https://nextjs.org/docs/app/api-reference/cli/next).
