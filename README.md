# Jack's Website

This is a website built with Nuxt using the Content Wind theme. I have made a few enhancements that are documented below. The original documentation is included at the bottom of this README.

## Aftermarket Updates

### Transitions

I added transitions page to the app. This enhancement improves the user experience as each page must be fully assembled before it is displayed. That way, the icons and images don't jiggle around and shift as you move from page to page. I upgraded to Nuxt 4 to do this.

I added this code to `nuxt.config.ts`:

```ts
  app: {
    pageTransition: { name: 'page', mode: 'out-in' },
  },
```

I added this code to the bottom of `app.vue`:

```vue
<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
}
</style>
```

To get transitions to work with this app's Markdown slug, I wrapped the `NuxtLayout` component in an `article` element. This prevents DOM errors.

```vue
<template>
  <article>
  <NuxtLayout :name="page?.layout as LayoutKey || 'default'" class="bg-white dark:bg-gray-800 ring-1 ring-gray-200 dark:ring-gray-700">
    <ContentRenderer
      v-if="page"
      :value="page"
      class="prose dark:prose-invert prose-pre:bg-gray-100 dark:prose-pre:bg-gray-900"
    />
  </NuxtLayout>
</article>
</template>
```


### Vite Sourcemap

I disabled the Vite sourcemap feature. When used with Tailwind, it triggered warnings during the build. This is a [known issue](https://github.com/tailwindlabs/tailwindcss/discussions/16119).

`nuxt.config.ts`

```ts
  vite: {
    build: {
      sourcemap: false, // Vite doesn't support Tailwind sourcemaps. This configuration suppresses the warning message in build.
    },
    plugins: [
      tailwindcss(),
    ],
  },
```


## Original Documentation

[![Content Wind](https://content-wind.nuxt.space/cover.jpg)](https://content-wind.nuxt.space)

### Content Wind

[![License][license-src]][license-href]
[![Nuxt][nuxt-src]][nuxt-href]
[![Nuxt Studio][nuxt-studio-src]][nuxt-studio-href]

A personal website theme powered by [Nuxt Content](https://content.nuxt.com), [TailwindCSS](https://tailwindcss.com), [Iconify](https://iconify.design) and [Vue components](https://vuejs.org).

- 📖&nbsp; [Demo & Docs](https://content-wind.nuxt.space)
- 🕹&nbsp; [Play online](https://githubblitz.com/Atinux/content-wind/tree/main/.demo)
- 👀&nbsp; [Demo video](https://twitter.com/Atinux/status/1578505586979012608)

#### Features

- Create pages in Markdown in the `content/` directory
- Use [Nuxt layouts](https://nuxt.com/docs/guide/directory-structure/layouts) in your Markdown pages
- Enjoy meta tag generation from Markdown files
- Configurable prose components with [Nuxt Typography](https://typography.nuxt.space)
- Generated navigation based on your pages
- Switch between Light & Dark mode :moon:
- Access 200,000 icons from 100+ icon sets with the `<Icon>` component
- Highlight code blocks with [Shiki](https://shiki.style)
- Create Vue components and use them in Markdown
- Deploy on any Node or Static hosting: GH Pages, Vercel, Netlify, Heroku, etc.
- Live edit on [Nuxt Studio](https://nuxt.studio)

#### Get started

##### Local

```bash
npx nuxi@latest init -t github:atinux/content-wind my-website
```

Then follow the instructions and you are ready to go :rocket:

#### License 📎

[MIT License](./LICENSE)

<!-- Badges -->
[license-src]: https://img.shields.io/github/license/Atinux/content-wind.svg?style=flat&colorA=18181B&colorB=28CF8D
[license-href]: https://github.com/Atinux/content-wind/blob/main/LICENSE

[use-template-src]: https://img.shields.io/badge/⚡️-Use%20this%20template-28CF8D?style=flat&colorA=18181B&colorB=28CF8D
[use-template-href]: https://github.com/Atinux/content-wind-template/generate

[nuxt-studio-src]: https://img.shields.io/badge/Open%20in%20Nuxt%20Studio-18181B?&logo=nuxt.js&logoColor=3BB5EC
[nuxt-studio-href]: https://nuxt.studio/templates/content-wind

[nuxt-src]: https://img.shields.io/badge/Nuxt-18181B?&logo=nuxt.js
[nuxt-href]: https://nuxt.com
