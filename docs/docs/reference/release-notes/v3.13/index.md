---
date: "2021-08-31"
version: "3.13.0"
title: "v3.13 Release Notes"
---

Welcome to `gatsby@3.13.0` release (August 2021 #3)

Key highlights of this release:

- [Improved Changelogs](#improved-changelogs) - Better structured and easier to read
- [`sharp` v0.29](#sharp-v029) - Reduced install size, improved encoding time, and improved AVIF image quality
- [Faster Sourcing for `gatsby-source-drupal`](#faster-sourcing-for-gatsby-source-drupal) - Speed up fetching data by around 4x
- [webpack Caching in Development for Everyone](#webpack-caching-in-development-for-everyone) - Activating it for all users

Also check out [notable bugfixes](#notable-bugfixes--improvements).

**Bleeding Edge:** Want to try new features as soon as possible? Install `gatsby@next` and let us know
if you have any [issues](https://github.com/gatsbyjs/gatsby/issues).

[Previous release notes](/docs/reference/release-notes/v3.12)

[Full changelog](https://github.com/gatsbyjs/gatsby/compare/gatsby@3.13.0-next.0...gatsby@3.13.0)

---

## Improved Changelogs

While the release notes (like the one you're reading right now) are hand-written and manually published, the changelog of each package we publish has been autogenerated by `lerna` in the past and unfortunately the generated output wasn't ideal for users to consume. We know that developers love detailed and accurate changelogs so we decided to replace `lerna` behavior with our own tooling. In [PR #32884](https://github.com/gatsbyjs/gatsby/pull/32886) we added these functionalities and the results are much better.

Take [`gatsby-plugin-image` changelog](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-image/CHANGELOG.md) as an example:

- Each semver release is its own heading (+ the date it was released)
- If applicable the general release notes are linked
- The PRs are categorized into features, bug fixes, chores, and other

## `sharp` v0.29

As always, thanks to [lovell](https://github.com/lovell) for maintaining `sharp` and sending in the [PR #32851](https://github.com/gatsbyjs/gatsby/pull/32851) to update `sharp` (see [`sharp` v0.29 changelog](https://sharp.pixelplumbing.com/changelog#v0290---17th-august-2021)) and our image plugins. `gatsby-plugin-sharp` now no longer uses `imagemin` but native `sharp` methods.

You'll get these benefits by upgrading:

- Reduced JPEG, PNG, and AVIF encoding time by up to 50%
- Reduced Gatsby install size/time by ~10% (~19MB smaller on filesystem)
- Improved AVIF image quality and will also work with Chrome 93+

## Faster Sourcing for `gatsby-source-drupal`

You now can significantly speed up sourcing from your Drupal instance if you install [JSON:API Extras](https://www.drupal.org/project/jsonapi_extras) and enable "Include count in collection queries" (`/admin/config/services/jsonapi/extras`). The [PR #32883](https://github.com/gatsbyjs/gatsby/pull/32883) leverages that information to enable parallel API requests.

For a test site with ~3200 entities and a warm Drupal cache (and no CDN cache), this change dropped sourcing time from 14s to 4s. On a very large production Drupal site (~600k entities), fetching time for a cold build dropped from 2 hours to 30 minutes 🚀.

## webpack Caching in Development for Everyone

After ramping up the opt-in of this feature to 20% in [v3.12](/docs/reference/release-notes/v3.12/#ramping-up-support-for-webpack-caching-in-development) we're now enabling this feature for everyone! So webpack 5 built-in persistent caching is now enabled for everyone both in development and production. It allows webpack to reuse results of previous compilations and significantly speed up those steps.

## Notable bugfixes & improvements

- `gatsby-source-drupal`: Provide an additional config option to specify entities that are not translatable to resolve to default language, via [PR #32548](https://github.com/gatsbyjs/gatsby/pull/32548)
- `gatsby`: Remove the `removeDimensions` option from svgo config, via [PR #32834](https://github.com/gatsbyjs/gatsby/pull/32834)
- `gatsby`: Hashes and anchors in redirects also work in production, via [PR #32850](https://github.com/gatsbyjs/gatsby/pull/32850)
- `gatsby-plugin-gatsby-cloud`: Always create the `redirect.json` file even if you remove all redirects, via [PR #32845](https://github.com/gatsbyjs/gatsby/pull/32845)
- `gatsby-remark-images`: Only convert supported image extensions, via [PR #32868](https://github.com/gatsbyjs/gatsby/pull/32868)
- `gatsby-source-wordpress`: Compatibility with Parallel Query Running (PQR), via [PR #32779](https://github.com/gatsbyjs/gatsby/pull/32779)
- `gatsby-core-utils`: Switch from deprecated `auth` option in `got` to `username`/`password`, via [PR #32665](https://github.com/gatsbyjs/gatsby/pull/32665)
- `gatsby`: Don't log `FAST_DEV` messages multiple times, via [PR #32961](https://github.com/gatsbyjs/gatsby/pull/32961)
- `gatsby`: Fix for "Static Query cannot be found" error, via [PR #32949](https://github.com/gatsbyjs/gatsby/pull/32949)

## Contributors

A big **Thank You** to [our community who contributed](https://github.com/gatsbyjs/gatsby/compare/gatsby@3.13.0-next.0...gatsby@3.13.0) to this release 💜

- [glennforrest](https://github.com/glennforrest): Fix typo of wether to whether [PR #32797](https://github.com/gatsbyjs/gatsby/pull/32797)
- [apmsooner](https://github.com/apmsooner): feat(gatsby-source-drupal): Default language when non translatable. [PR #32548](https://github.com/gatsbyjs/gatsby/pull/32548)
- [jonniebigodes](https://github.com/jonniebigodes): chore(docs): Update Storybook guide with Addon [PR #32793](https://github.com/gatsbyjs/gatsby/pull/32793)
- [bytrangle](https://github.com/bytrangle)

  - chore(docs): Remark plugin, add tip for gatsby clean [PR #32822](https://github.com/gatsbyjs/gatsby/pull/32822)
  - chore(docs): Change example for using async in Remark plugin [PR #32874](https://github.com/gatsbyjs/gatsby/pull/32874)
  - chore(docs): Add hint for MDX plugin in remark-plugin-tutorial [PR #32876](https://github.com/gatsbyjs/gatsby/pull/32876)

- [vanessayuenn](https://github.com/vanessayuenn): chore(docs): Add title for image-plugin-architecture [PR #32803](https://github.com/gatsbyjs/gatsby/pull/32803)
- [mundry](https://github.com/mundry): chore(docs): Fix typos throughout docs [PR #32807](https://github.com/gatsbyjs/gatsby/pull/32807)
- [nategiraudeau](https://github.com/nategiraudeau): docs(gatsby-source-contentful) provide a code example for rendering rich-text embedded assets images [PR #32777](https://github.com/gatsbyjs/gatsby/pull/32777)
- [Zemnmez](https://github.com/Zemnmez): gatsby-plugin-image: bump do-sync to v3 [PR #32808](https://github.com/gatsbyjs/gatsby/pull/32808)
- [Dgiordano33](https://github.com/Dgiordano33): chore(docs): Change Jamstack Article [PR #32764](https://github.com/gatsbyjs/gatsby/pull/32764)
- [SwiftWinds](https://github.com/SwiftWinds): chore(docs): Fix typo in v3.0 release notes [PR #32844](https://github.com/gatsbyjs/gatsby/pull/32844)
- [ashiishme](https://github.com/ashiishme): chore(docs): Remove outdated information from Theme Guide [PR #32849](https://github.com/gatsbyjs/gatsby/pull/32849)
- [facundojmaero](https://github.com/facundojmaero): chore(docs): Fix typo in part 5 of the tutorial [PR #32854](https://github.com/gatsbyjs/gatsby/pull/32854)
- [herecydev](https://github.com/herecydev): fix(gatsby): Correct server type [PR #32853](https://github.com/gatsbyjs/gatsby/pull/32853)
- [torn4dom4n](https://github.com/torn4dom4n): chore(docs): Fixes typo in tutorial part 4 [PR #32859](https://github.com/gatsbyjs/gatsby/pull/32859)
- [lovell](https://github.com/lovell): feat(gatsby-plugin-sharp): reduce encoding time and install size [PR #32851](https://github.com/gatsbyjs/gatsby/pull/32851)
- [frankpengau](https://github.com/frankpengau): chore(docs): Update Gallery example in tutorial part 2 [PR #32872](https://github.com/gatsbyjs/gatsby/pull/32872)
- [AnilSeervi](https://github.com/AnilSeervi)

  - chore(docs): Fix CSS Modules extension typo [PR #32869](https://github.com/gatsbyjs/gatsby/pull/32869)
  - chore(docs): Fix code highlighting in part 6 [PR #32900](https://github.com/gatsbyjs/gatsby/pull/32900)

- [moinulmoin](https://github.com/moinulmoin): chore(docs): Fix typo in tutorial part 6 [PR #32866](https://github.com/gatsbyjs/gatsby/pull/32866)
- [Mike-Dax](https://github.com/Mike-Dax): chore(gatsby-remark-images): Only convert supported image extensions [PR #32868](https://github.com/gatsbyjs/gatsby/pull/32868)
- [jablko](https://github.com/jablko): fix(gatsby): add react-com as devDep [PR #32865](https://github.com/gatsbyjs/gatsby/pull/32865)
- [barrymcgee](https://github.com/barrymcgee): Update docs on building eCom with Shopify to work with latest versions [PR #32884](https://github.com/gatsbyjs/gatsby/pull/32884)
- [jfrosch](https://github.com/jfrosch): chore(docs): Update wording for "using-web-fonts" [PR #32902](https://github.com/gatsbyjs/gatsby/pull/32902)
- [alvis](https://github.com/alvis): fix(gatsby): add this typings to actions [PR #32210](https://github.com/gatsbyjs/gatsby/pull/32210)
- [satrix321](https://github.com/satrix321): fix(gatsby-core-utils): Switch `auth` option from got to username/password [PR #32665](https://github.com/gatsbyjs/gatsby/pull/32665)
