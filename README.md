[中文](./README_zh.md)

# nuxt-toc

[![npm version][npm-version-src]][npm-version-href]
[![npm downloads][npm-downloads-src]][npm-downloads-href]
[![License][license-src]][license-href]
[![Nuxt][nuxt-src]][nuxt-href]

<div align="center">
  <img src="./logo.png" alt="logo" width="150">
</div>

A Nuxt module for table of contents (TOC) component in your Nuxt Content projects.



- [✨  Release Notes](https://github.com/hanyujie2002/nuxt-toc/releases)
<!-- - 🏀 Online playground -->
<!-- - 📖  Documentation -->

## Features ✨

- 🎨 **Highly Customizable**: Tailor it to fit your unique needs.
- 🔍 **Active TOC Highlighting**: Easily see which section you're in.
- 📦 **Out of the Box**: Ready to use with minimal setup.
- 🔗 **Section Links**: Navigate seamlessly within your content.

## Quick Start 🔧

1. Install the module to your Nuxt application with one command:

```bash
npx nuxi module add nuxt-toc
```

2. Add `<TableOfContents />` at where TOC is needed.

```vue
<template>
    <ContentDoc />
    <TableOfContents />
</template>
```

## Props

| **Prop**           | **Type** | **Default** | **Description**                                                                                     |
|--------------------|----------|-------------|-----------------------------------------------------------------------------------------------------|
| `path`             | String   | `''`        | The path to the content for which the TOC is generated. **If not set, `nuxt-toc` will default to using the current URI as the path**.                                    |
| `isSublistShown`   | Boolean  | `true`      | Determines whether the sublist within the TOC is shown.                                             |
| `isTitleShownWithNoContent` | Boolean  | `false`     | Determines whether the title is shown even if there is no content in the TOC.                                  |
| `title`            | String   | `'Table of Contents'` | The title of the TOC.                                                                               |

## Styling

| **ID/Class**                | **Type** | **Description**                                                                                     |
|-----------------------------|----------|-----------------------------------------------------------------------------------------------------|
| `toc-container`             | ID       | The container for the table of contents (TOC).                                                      |
| `toc-title`                 | ID       | The title of the table of contents.                                                                 |
| `toc-item`                  | Class    | General class for TOC items.                                                                        |
| `toc-topitem`               | Class    | Specific class for top-level TOC items.                                                             |
| `active-toc-item`           | Class    | Applied to active TOC items.                                                                        |
| `active-toc-topitem`        | Class    | Applied to active top-level TOC items.                                                              |
| `toc-link`                  | Class    | General class for TOC links.                                                                        |
| `toc-toplink`               | Class    | Specific class for top-level TOC links.                                                             |
| `active-toc-link`           | Class    | Applied to active TOC links.                                                                        |
| `active-toc-toplink`        | Class    | Applied to active top-level TOC links.                                                              |
| `toc-sublist`               | Class    | Styles the sublist within the TOC.                                                                  |
| `toc-subitem`               | Class    | Specific class for sub-level TOC items.                                                             |
| `active-toc-subitem`        | Class    | Applied to active sub-level TOC items.                                                              |
| `toc-sublink`               | Class    | Specific class for sub-level TOC links.                                                             |
| `active-toc-sublink`        | Class    | Applied to active sub-level TOC links.                                                              |
| `toc-item-${link.id}`       | ID       | Dynamically generated ID for each TOC item, based on the `link.id`.                                 |
| `toc-topitem-and-sublist`   | Class    | Styles the top-level TOC items and their sublists.                                                  |

> [!NOTE]
> The default styling of the `<TableOfContents />` component is:
>
> ```css
> .active-toc-item {
>   color: #fef08a;
> }
>
> .toc-sublist-item {
>   padding-left: 1rem;
> }
> ```
>
> You can customize the style or reset it with:
>
> ```css
> .active-toc-item {
>   color: inherit;
> }
>
> .toc-sublist-item {
>   padding-left: 0;
> }
> ```

## Cookbook

### Example One

Custom color for active items and custom padding for subitems

```vue
<template>
    <ContentDoc />
    <TableOfContents />
</template>

<style>
/* Styling for active Table of Contents items */
.active-toc-item {
  color: #4ade80;
}

/* Indentation for second-level Table of Contents items */
.toc-sublist-item {
  padding-left: 1.5rem;
}
</style>

<!-- Or with Tailwind CSS
<style>
.active-toc-item {
  @apply bg-green-300
}

.toc-sublist-item {
  @apply pl-1.5
}
</style>
-->
```

Result:

<div align="center">
  <img src="./screenshots/example.png" alt="example">
</div>

### Example Two

Having a bar at left of each item

```vue
<template>
    <ContentDoc />
    <TableOfContents />
</template>

<style>
.toc-item {
  border-left-width: 2px;
  padding-left: 0.25rem /* 4px */;
}

.active-toc-item {
  color: #60a5fa;
  border-color: #60a5fa;
}

.toc-sublist-item {
  padding-left: 1rem;
}
</style>

<!-- Or with Tailwind CSS
<style>
.toc-item {
  @apply border-l-2 pl-1
}

.active-toc-item {
  @apply text-blue-400 border-blue-400
}

.toc-sublist-item {
  @apply pl-4
}
</style>
-->
```

Result:

<div align="center">
  <img src="./screenshots/example1.png" alt="example1">
</div>

### Example Three

First level titles be active when any of it's second level titles be active.

```vue
<template>
    <ContentDoc />
    <TableOfContents />
</template>

<style>
.active-toc-item {
  /* Overrides builtin style */
  color: inherit;
}

/* Sublist item is contained in sub list, which is top item's sibling */
.active-toc-item, .toc-topitem:has(+ .toc-sublist .active-toc-sublist-item) {
  color: #60a5fa
}

.active-toc-sublist-item {
  color: #4ade80
}

.toc-sublist-item {
  padding-left: 1rem /* 16px */;
}
</style>

<!-- Or with Tailwind CSS
<style>
.active-toc-item {
  @apply text-inherit
}

.active-toc-item, .toc-topitem:has(+ .toc-sublist .active-toc-sublist-item) {
  @apply text-blue-400
}

.active-toc-sublist-item {
  @apply text-green-400
}

.toc-sublist-item {
  @apply pl-4
}
</style>
-->
```

Result:

<div align="center">
  <img src="./screenshots/example2.png" alt="example2">
</div>

[npm-version-src]: https://img.shields.io/npm/v/nuxt-toc/latest.svg?style=flat&colorA=020420&colorB=00DC82
[npm-version-href]: https://npmjs.com/package/nuxt-toc

[npm-downloads-src]: https://img.shields.io/npm/dm/nuxt-toc.svg?style=flat&colorA=020420&colorB=00DC82
[npm-downloads-href]: https://npmjs.com/package/nuxt-toc

[license-src]: https://img.shields.io/npm/l/nuxt-toc.svg?style=flat&colorA=020420&colorB=00DC82
[license-href]: https://npmjs.com/package/nuxt-toc

[nuxt-src]: https://img.shields.io/badge/Nuxt-020420?logo=nuxt.js
[nuxt-href]: https://nuxt.com
