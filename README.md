<h1 align='center'>zHead</h1>

<p align="center">
<a href='https://github.com/harlan-zw/zhead/actions/workflows/test.yml'>
<img src='https://github.com/harlan-zw/zhead/actions/workflows/test.yml/badge.svg' >
</a>
<a href="https://www.npmjs.com/package/zhead" target="__blank"><img src="https://img.shields.io/npm/v/zhead?color=2B90B6&label=" alt="NPM version"></a>
<a href="https://www.npmjs.com/package/zhead" target="__blank"><img alt="NPM Downloads" src="https://img.shields.io/npm/dm/zhead?color=349dbe&label="></a>
<br>
<a href="https://github.com/harlan-zw/zhead" target="__blank"><img alt="GitHub stars" src="https://img.shields.io/github/stars/harlan-zw/zhead?style=social"></a>
</p>

<p align="center">
Fully typed utilities for defining, validating and building best-practice document &lt;head&gt;'s.  
</p>

<p align="center">
<table>
<tbody>
<td align="center">
<img width="800" height="0" /><br>
<i>Status:</i> In Development</b> <br>
<sup> Please report any issues 🐛</sup><br>
<sub>Made possible by my <a href="https://github.com/sponsors/harlan-zw">Sponsor Program 💖</a><br> Follow me <a href="https://twitter.com/harlan_zw">@harlan_zw</a> 🐦 • Join <a href="https://discord.gg/275MBUBvgP">Discord</a> for help</sub><br>
<img width="800" height="0" />
</td>
</tbody>
</table>
</p>

## Features

- 💎 Fully typed, [Zod-powered](https://zod.dev/) Schema with optional validation
- 🧙 Resolve typed, flat meta tags, e.g. ` { ogTitle: 'Test', robots: { maxSnippet: -1 } }`
- 📦 Supports camelCase'd keys `dataSomething` -> `data-something`
- ✨ Generate minimal tags with maximum SEO `buildSeoHead`
- ✍️ Render to HTML and [useHead](https://github.com/vueuse/head) compatible tags
- 🌳 Composable, tree-shakable and tiny (< 1kb)

## Installation

```bash
npm add zhead
```

## API

### defineHead

Use this decorator for a simple fully-typed head schema. 

By default, it will only allow camelCase keys, you can convert them at runtime using `resolveHead.`

```ts
import { defineHead } from 'zhead'

const head = defineHead({
  title: 'My Page',
})

// {
//    title: 'My Page',
// }
```

### resolveHead

Use the `resolveHead` function to convert any camel-cased keys to a casing that browsers will understand..

```ts
import { resolveHead } from 'zhead'

const head = resolveHead({
  meta: [
    { httpEquiv: 'content-security-policy', content: 'content-src none' }
  ]
})
// {
//   meta: [
//     { 'http-equiv': 'content-security-policy', content: 'content-src none' }
//   ]
// }
```

### resolveMetaFlat

Use this function to describe your meta tags with a flat fully-typed, object.

```ts
import { defineHead, resolveMetaFlat } from 'zhead'

const head = defineHead({
  meta: resolveMetaFlat({
    httpEquiv: 'content-src none',
  })
})
// {
//   meta: [
//     { 'http-equiv': 'content-security-policy', content: 'content-src none' }
//   ]
// }
```

### resolveSeoHead

Use this function to generate a minimal SEO head with maximum SEO.

Internally this function uses the `withDefaults` and `inferSocialShare` utilities.

```ts
import { resolveSeoHead, resolveMetaFlat } from 'zhead'

const head = resolveSeoHead({
  title: 'Learn about zHead - zHead',
  description: 'Describing the basic usage of zHead.',
})

// {
//   "title": "My Title",
//   "meta": [
//     {
//       "content": "Some description",
//       "name": "description",
//     },
//     {
//       "charset": "utf-8",
//     },
//     {
//       "content": "initial-scale=1, width=device-width",
//       "name": "viewport",
//     },
//     {
//       "content": "My Title",
//       "property": "og:title",
//     },
//     {
//       "content": "Some description",
//       "property": "og:description",
//     },
//     {
//       "content": "max-snippet:-1, max-image-preview:large, max-video-preview:-1",
//       "name": "robots",
//     },
//   ],
// }
```

### generateHtml

```ts
import { generateHtml } from 'zhead'

const html = generateHtml({
  title: 'test',
  script: [
    { src: 'https://example.com/script.js' },
  ],
  meta: [
    { name: 'description', content: 'test' },
  ]
})

// <title>test</title>
// <meta content="test" name="description">
// <script src="https://example.com/script.js"></script>
```

### generateTags

```ts
import { generateTags } from 'zhead'

const tags = generateTags({
  title: 'test',
  script: [
    { src: 'https://example.com/script.js' },
  ],
  meta: [
    { name: 'description', content: 'test' },
  ]
})

// [
//   {
//     "props": {
//       "children": "test",
//     },
//     "tag": "title",
//   },
//   {
//     "props": {
//       "content": "test",
//       "name": "description",
//     },
//     "tag": "meta",
//   },
//   {
//     "props": {
//       "src": "https://example.com/script.js",
//     },
//     "tag": "script",
//   },
// ]
```

## Sponsors

<p align="center">
  <a href="https://raw.githubusercontent.com/harlan-zw/static/main/sponsors.svg">
    <img src='https://raw.githubusercontent.com/harlan-zw/static/main/sponsors.svg'/>
  </a>
</p>


## License

MIT License © 2022-PRESENT [Harlan Wilton](https://github.com/harlan-zw)
