---
name: nextjs-turbopack
description: Next.js 16+ and Turbopack — incremental bundling, FS caching, dev speed, and when to use Turbopack vs webpack.
origin: ECC
---

# Next.js ve Turbopack

Next.js 16+ hem yerel geliştirme hem de production build için varsayılan olarak Turbopack kullanır. Rust ile yazılmış artımlı bir bundler’dır.

## Ne Zaman Kullanılır

- **Turbopack (varsayılan dev)**: Günlük geliştirme için kullanın. Özellikle büyük uygulamalarda daha hızlı soğuk başlatma ve HMR.
- **Webpack alternatifi**: Webpack uyumluluğu için `next dev --webpack` veya `next build --webpack` kullanın.
- **Production**: Next.js 16+ sürümünde `next build` varsayılan olarak Turbopack kullanır; webpack için `--webpack` ekleyin.

Şu durumlarda kullanın: Next.js 16+ uygulamalarını geliştirme veya debug etme, yavaş dev başlatma veya HMR'yi teşhis etme veya production bundle'larını optimize etme.

## Nasıl Çalışır

- **Turbopack**: Next.js geliştirme ve production build için artımlı bundler.
- **Varsayılan bundler**: Next.js 16’dan itibaren hem `next dev` hem de `next build` varsayılan olarak Turbopack kullanır.
- **Dosya sistemi önbelleği**: Next.js 16.0’da geliştirme önbelleği beta’dır ve `experimental.turbopackFileSystemCacheForDev: true` gerektirir. 16.1’den itibaren geliştirme önbelleği kararlıdır ve varsayılan olarak açıktır. Bu sürüm sınırları build önbelleğine değil, geliştirme önbelleğine aittir.
- **Bundle Analyzer (Next.js 16.1+)**: Bundle’ları ve büyük bağımlılıkları incelemek için `next experimental-analyze` çalıştırın. Bu komut uygulama build’i üretmez.

## Örnekler

### Komutlar

```bash
next dev
next build
next start
```

### Kullanım

Turbopack ile yerel geliştirme için `next dev` çalıştırın. Code-splitting'i optimize etmek ve büyük bağımlılıkları kırpmak için Bundle Analyzer'ı kullanın (Next.js dokümantasyonuna bakın). Mümkün olduğunda App Router ve server component'leri tercih edin.

## En İyi Uygulamalar

- Kararlı Turbopack ve önbellekleme davranışı için güncel bir Next.js 16.x sürümünde kalın.
- Dev yavaşsa, Turbopack'te (varsayılan) olduğunuzdan ve önbelleğin gereksiz yere temizlenmediğinden emin olun.
- Production bundle boyutu sorunları için, sürümünüz için resmi Next.js bundle analiz araçlarını kullanın.

References: [Next.js 16](https://nextjs.org/blog/next-16), [Next.js 16.1](https://nextjs.org/blog/next-16-1), [Next.js CLI](https://nextjs.org/docs/app/api-reference/cli/next).
