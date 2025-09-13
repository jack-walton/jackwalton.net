# Jack's Website

[![License][license-src]][license-href]
[![Nuxt][nuxt-src]][nuxt-href]

This is a website built with Nuxt using the Content Wind theme. I have made a few enhancements that are documented below. For the original template and documentation, see [antinux/content-wind](https://github.com/atinux/content-wind).

## Install the Website Locally

## Icons

Use icons in Markdown like this, where **icon name** is the name of the icon in particular:

```md
:icon{name="icon-name"}
```

You can use any icon from the [Iconify](https://iconify.design/) sets. Copy the name of the icon you want to use.  You can also use the `<Icon>` Nuxt component.

For the best user experience, download the icon set you plan to use and install it directly in the app.

## Tailwind CSS

This website uses the [TailwindCSS](https://tailwindcss.com) framework. You can learn more about how to customize the appearance of the website in the [Tailwind docs](https://tailwindcss.com/docs/installation/framework-guides/nuxt).

## Dark Mode

I removed the toggle switch code from the `AppNavBar` component:

```vue
<ColorModeSwitch class="dark:text-gray-100 hover:text-gray-700 dark:hover:text-gray-300" />

```

I also broke up the colors in the `main.css` stylesheet so that dark mode and light mode automatically responds to the user's system preferences rather than a toggle.

## Transitions

I added page transitions to the app. This enhancement improves the user experience as each page must be fully assembled before it is displayed. That way, the icons and images don't jiggle around and shift as you move from page to page. I upgraded to Nuxt 4 to do this.

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


## Vite Sourcemap

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

## Nuxt Studio
[![Nuxt Studio][nuxt-studio-src]][nuxt-studio-href]. Live edit on [Nuxt Studio](https://content.nuxt.com).

You can use Nuxt Studio to develop this website. 

## Nuxt Content

This website uses [Nuxt Content] and can function as a headless CMS. You can learn more about that in the [Nuxt Content docs](https://content.nuxt.com/docs/getting-started/installation).

## Develop Content

Create pages in Markdown in the `content/` directory. You can configure prose components with [Nuxt Typography](https://typography.nuxt.space). You can add basic metadata in the front matter of the Markdown files:

```
---
navigation:
  title: Notes
layout: full-width
seo:
  description: This is a page where I write long posts.
  image: /cover.jpg'
---
```

## Navigation

The navigation element places the Markdown files in numerical order from left to right. You can theoretically have as many pages as you want, but the links will wrap around and stack on top of each other if you use too many pages. Three files seems to be the ideal amount.

## Nuxt Layouts

This application currently uses two [Nuxt layouts](https://nuxt.com/docs/4.x/guide/directory-structure/app/layouts). You can define which is used in the Markdown front matter.

## Syntax Highlighting

You can highlight code blocks with [Shiki](https://shiki.style).

## Markdown Component Syntax

You can create [Vue components](https://vuejs.org) and use them in the Markdown files.

## License

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
