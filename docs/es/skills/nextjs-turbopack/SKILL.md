---
name: nextjs-turbopack
description: Next.js 16+ y Turbopack — bundling incremental, caché en sistema de archivos, velocidad de desarrollo y cuándo usar Turbopack frente a webpack.
origin: ECC
---

# Next.js y Turbopack

Next.js 16+ usa Turbopack por defecto tanto para el desarrollo local como para los builds de producción. Es un bundler incremental escrito en Rust.

## Cuándo Usar

- **Turbopack (desarrollo por defecto)**: Usar para el desarrollo diario. Inicio en frío y HMR más rápidos, especialmente en apps grandes.
- **Alternativa webpack**: Para compatibilidad con webpack, usar `next dev --webpack` o `next build --webpack`.
- **Producción**: En Next.js 16+, `next build` usa Turbopack por defecto; `--webpack` permite optar por webpack.

Usar cuando: se desarrollen o depuren apps Next.js 16+, se diagnostique un inicio de desarrollo lento o HMR, o se optimicen bundles de producción.

## Cómo Funciona

- **Turbopack**: Bundler incremental para el desarrollo y los builds de producción de Next.js.
- **Bundler por defecto**: Desde Next.js 16, tanto `next dev` como `next build` usan Turbopack por defecto.
- **Caché en sistema de archivos**: En Next.js 16.0, la caché de desarrollo es beta y requiere `experimental.turbopackFileSystemCacheForDev: true`. Desde 16.1, es estable y está habilitada por defecto. Estos límites de versión se refieren a la caché de desarrollo, no a la de builds.
- **Bundle Analyzer (Next.js 16.1+)**: Ejecutar `next experimental-analyze` para inspeccionar bundles y encontrar dependencias pesadas. Este comando no genera un build de la aplicación.

## Ejemplos

### Comandos

```bash
next dev
next build
next start
```

### Uso

Ejecutar `next dev` para el desarrollo local con Turbopack. Usar el Bundle Analyzer (ver documentación de Next.js) para optimizar el code-splitting y eliminar dependencias grandes. Preferir App Router y server components donde sea posible.

## Nomenclatura del Archivo de Middleware

Next.js 16 introdujo `proxy.ts` como nombre del archivo de middleware, reemplazando la convención anterior de `middleware.ts`:

- **Next.js 16+**: usar `proxy.ts` en la raíz del proyecto o dentro de `src`, al mismo nivel que `app` o `pages`
- **Anterior a Next.js 16**: usar `middleware.ts` en la raíz del proyecto o dentro de `src`, al mismo nivel que `app` o `pages`

El cambio de nombre de archivo está vinculado a la **versión de Next.js**, no al bundler que se usa (Turbopack o webpack). Siempre consultar la documentación oficial para la versión que se está revisando.

**No marcar `proxy.ts` como un archivo de middleware mal nombrado o faltante en proyectos Next.js 16.** El archivo es correcto e intencional. `middleware.ts` está deprecado, pero sigue siendo compatible con Next.js 16. No renombrar estos archivos solo por el bundler utilizado.

## Buenas Prácticas

- Mantenerse en una versión reciente de Next.js 16.x para un comportamiento estable de Turbopack y caché.
- Si el desarrollo es lento, asegurarse de estar usando Turbopack (predeterminado) y que la caché no se esté borrando innecesariamente.
- Para problemas de tamaño de bundle en producción, usar las herramientas oficiales de análisis de bundle de Next.js para tu versión.

References: [Next.js 16](https://nextjs.org/blog/next-16), [Next.js 16.1](https://nextjs.org/blog/next-16-1), [Next.js CLI](https://nextjs.org/docs/app/api-reference/cli/next).
