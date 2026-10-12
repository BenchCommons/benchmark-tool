# GitHub Actions ubuntu-24.04, one runner per generator

- Environment: GitHub Actions ubuntu-24.04, one runner per generator
- Started: 2026-10-11 03:14:03 UTC
- Completed: 2026-10-11 10:15:01 UTC
- Commit: 4c6e185b5b4a72c9779a722800b1133ff23bebdd

Suite: GG v1 · cell 1/2 (nf 100000, cs 5) · profile core · resources 4 CPU / 8.0 GB

| Framework | Language | Files | Size (KB) | Min runs | Mean (s) | Stddev (s) | Median (s) | Min (s) | Max (s) | Status | Rank | CV | Posts/s | MB/s | CPU (cores) | Peak RSS (MB) | Output (MB / files) | Image build (s) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| zola | rust | 100000 | 5 | 1 | 38.774 | — | 38.774 | 38.774 | 38.774 | ok | 1 | — | 2579.0 | 13.8 | 1.86 | 7195.8 | 892.7 / 100008 | 24.7 |
| jekyll | ruby | 100000 | 5 | 1 | 85.585 | — | 85.585 | 85.585 | 85.585 | ok | 1 | — | 1168.4 | 6.2 | 0.99 | 2271.4 | 1117.7 / 100001 | 53.1 |
| hugo | go | 100000 | 5 | 1 | 152.838 | — | 152.838 | 152.838 | 152.838 | ok | 1 | — | 654.3 | 3.5 | 3.14 | 6700.6 | 1231.3 / 100003 | 27.7 |
| astro | javascript | 100000 | 5 | 1 | 185.432 | — | 185.432 | 185.432 | 185.432 | ok | 2 | — | 539.3 | 2.9 | 1.69 | 6705.0 | 1042.8 / 100001 | 43.3 |
| bridgetown | ruby | 100000 | 5 | 1 | 208.884 | — | 208.884 | 208.884 | 208.884 | ok | 1 | — | 478.7 | 2.6 | 0.83 | 5468.7 | 1113.1 / 100004 | 216.4 |
| jigsaw | php | 100000 | 5 | 1 | 421.472 | — | 421.472 | 421.472 | 421.472 | ok | 3 | — | 237.3 | 1.3 | 0.98 | 3655.4 | 929.9 / 100003 | 80.9 |
| nesta | ruby | 100000 | 5 | 1 | 520.601 | — | 520.601 | 520.601 | 520.601 | ok | 1 | — | 192.1 | 1.0 | 1.00 | 2532.5 | 978.6 / 100006 | 42.1 |
| lektor | python | 100000 | 5 | 1 | 548.534 | — | 548.534 | 548.534 | 548.534 | ok | 2 | — | 182.3 | 0.9 | 0.90 | 1137.8 | 831.4 / 100004 | 41.9 |
| franklin | julia | 100000 | 5 | 1 | 705.425 | — | 705.425 | 705.425 | 705.425 | ok | 3 | — | 141.8 | 0.7 | 0.91 | 7791.0 | 1179.2 / 100005 | 184.0 |
| mkdocs | python | 100000 | 5 | 1 | 914.132 | — | 914.132 | 914.132 | 914.132 | ok | 2 | — | 109.4 | 0.6 | 0.99 | 2689.8 | 904.1 / 100001 | 43.3 |
| middleman | ruby | 100000 | 5 | 1 | 936.635 | — | 936.635 | 936.635 | 936.635 | ok | 4 | — | 106.8 | 0.6 | 3.02 | 2253.0 | 1002.2 / 100002 | 104.7 |
| pelican | python | 100000 | 5 | 1 | 1061.888 | — | 1061.888 | 1061.888 | 1061.888 | ok | 5 | — | 94.2 | 0.5 | 1.00 | 1052.9 | 744.4 / 100001 | 44.0 |
| antora | javascript | 100000 | 5 | 1 | 1209.334 | — | 1209.334 | 1209.334 | 1209.334 | ok | 4 | — | 82.7 | 0.4 | 1.10 | 5541.0 | 1982.1 / 100003 | 36.3 |
| lustre-ssg | gleam | 100000 | 5 | 1 | 1495.995 | — | 1495.995 | 1495.995 | 1495.995 | ok | 1 | — | 66.8 | 0.4 | 1.09 | 6683.4 | 950.0 / 100004 | 21.9 |
| hakyll | haskell | 100000 | 5 | 1 | 1669.593 | — | 1669.593 | 1669.593 | 1669.593 | ok | 6 | — | 59.9 | 0.3 | 3.05 | 5025.0 | 1074.9 / 100003 | 2428.2 |
| nikola-mako | python | 100000 | 5 | 1 | 2254.696 | — | 2254.696 | 2254.696 | 2254.696 | ok | 7 | — | 44.4 | 0.2 | 1.00 | 3829.9 | 861.0 / 100025 | 51.8 |
| publish | swift | 100000 | 5 | 1 | 2459.651 | — | 2459.651 | 2459.651 | 2459.651 | ok | 8 | — | 40.7 | 0.2 | 1.01 | 2287.7 | 947.2 / 100004 | 135.6 |
| nanoc | ruby | 100000 | 5 | 1 | 2787.180 | — | 2787.180 | 2787.180 | 2787.180 | ok | 1 | — | 35.9 | 0.2 | 0.99 | 5373.0 | 1008.7 / 100001 | 46.8 |
| analog | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 64.0 |
| cecil | php | 100000 | 5 | — | — | — | — | — | — | timeout | — | — | — | — | — | — | — | 50.1 |
| cobalt | rust | 100000 | 5 | — | — | — | — | — | — | timeout | — | — | — | — | — | — | — | 26.1 |
| cryogen | clojure | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 49.9 |
| docfx | c# | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 48.6 |
| docmd | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 43.6 |
| docusaurus | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 86.5 |
| dumi | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 94.8 |
| eleventy | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 35.0 |
| emanote | haskell | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 3117.0 |
| gatsby | javascript | 100000 | 5 | — | — | — | — | — | — | timeout | — | — | — | — | — | — | — | 239.3 |
| hexo | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 41.7 |
| iles | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 43.1 |
| ink | go | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 56.2 |
| jbake | java | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 33.1 |
| laika | scala | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 48.0 |
| lume | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 33.3 |
| marmite | rust | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 61.7 |
| mdbook | rust | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 26.4 |
| metalsmith-handlebars | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 40.0 |
| metalsmith-nunjucks | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 37.6 |
| nextjs-export | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 56.0 |
| nextra | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 76.7 |
| nimib | nim | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 75.4 |
| nuxt-content | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 59.7 |
| observable-framework | javascript | 100000 | 5 | — | — | — | — | — | — | timeout | — | — | — | — | — | — | — | 45.6 |
| plenti | go | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 86.8 |
| quarkdown | kotlin | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 38.4 |
| quarto | typescript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 39.9 |
| quartz | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 274.9 |
| rspress | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 40.9 |
| sculpin | php | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 74.1 |
| soupault | ocaml | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 30.5 |
| sphinx | python | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 51.4 |
| starlight | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 51.5 |
| statiq | c# | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 64.2 |
| sveltekit | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 37.3 |
| tableau | elixir | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 82.2 |
| tanstack-start | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 44.5 |
| vike | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 41.7 |
| vite-ssg | javascript | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 39.5 |
| vitepress | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 41.7 |
| vuepress | javascript | 100000 | 5 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 44.9 |
| zensical | python | 100000 | 5 | — | — | — | — | — | — | timeout | — | — | — | — | — | — | — | 47.8 |
| zine | zig | 100000 | 5 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 26.0 |

## Ranking

Ordered by median; generators whose min–max ranges overlap share a rank (`=n`). Only results of the same suite, cell, profile, fingerprint and feature set are ranked together.

### GG v1 · nf 100000, cs 5 · profile core · fingerprint 3f2f1aaf006c

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | zola | 38.774 | — | 38.774–38.774 |
| 2 | astro | 185.432 | — | 185.432–185.432 |
| 3 | jigsaw | 421.472 | — | 421.472–421.472 |
| 4 | middleman | 936.635 | — | 936.635–936.635 |
| 5 | pelican | 1061.888 | — | 1061.888–1061.888 |
| 6 | hakyll | 1669.593 | — | 1669.593–1669.593 |
| 7 | nikola-mako | 2254.696 | — | 2254.696–2254.696 |
| 8 | publish | 2459.651 | — | 2459.651–2459.651 |

### GG v1 · nf 100000, cs 5 · profile core · fingerprint e2d6f2db677c

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | jekyll | 85.585 | — | 85.585–85.585 |

### GG v1 · nf 100000, cs 5 · profile core · fingerprint ba134637a49c

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | hugo | 152.838 | — | 152.838–152.838 |
| 2 | mkdocs | 914.132 | — | 914.132–914.132 |

### GG v1 · nf 100000, cs 5 · profile core · fingerprint 8e17af3b158e

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | bridgetown | 208.884 | — | 208.884–208.884 |

### GG v1 · nf 100000, cs 5 · profile core · fingerprint ebe58c534103

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | nesta | 520.601 | — | 520.601–520.601 |
| 2 | lektor | 548.534 | — | 548.534–548.534 |
| 3 | franklin | 705.425 | — | 705.425–705.425 |
| 4 | antora | 1209.334 | — | 1209.334–1209.334 |

### GG v1 · nf 100000, cs 5 · profile core · fingerprint de731ab3b8a5

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | lustre-ssg | 1495.995 | — | 1495.995–1495.995 |

### GG v1 · nf 100000, cs 5 · profile core · fingerprint 2bb7b205c77e

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | nanoc | 2787.180 | — | 2787.180–2787.180 |

## Caveats

- T9: oom means the generator exceeded the container memory limit, which is the same for every generator; it is an outcome, not a time.
- T7: peak RSS is the largest single process, not the sum, so it under-reports multi-process generators.

## Failed / timeout / oom / nonconformant / unsupported

- analog (oom): oom
- cecil (timeout): timeout
- cobalt (timeout): timeout
- cryogen (failed): SSGBERK_VERIFY_FAIL expected=100000 got=0
- docfx (failed): SSGBERK_VERIFY_FAIL build exited 255
- docmd (failed): SSGBERK_VERIFY_FAIL build exited 134
- docusaurus (oom): oom
- dumi (failed): SSGBERK_VERIFY_FAIL build exited 134
- eleventy (failed): SSGBERK_VERIFY_FAIL build exited 134
- emanote (oom): oom
- gatsby (timeout): timeout
- hexo (failed): SSGBERK_VERIFY_FAIL build exited 134
- iles (failed): SSGBERK_VERIFY_FAIL build exited 1
- ink (failed): SSGBERK_VERIFY_FAIL build exited 126
- jbake (failed): SSGBERK_VERIFY_FAIL build exited 134
- laika (failed): SSGBERK_VERIFY_FAIL build exited 1
- lume (failed): SSGBERK_VERIFY_FAIL build exited 133
- marmite (oom): oom
- mdbook (oom): oom
- metalsmith-handlebars (failed): SSGBERK_VERIFY_FAIL build exited 1
- metalsmith-nunjucks (failed): SSGBERK_VERIFY_FAIL build exited 1
- nextjs-export (failed)
- nextra (oom): oom
- nimib (failed): SSGBERK_VERIFY_FAIL build exited 139
- nuxt-content (failed): SSGBERK_VERIFY_FAIL build exited 1
- observable-framework (timeout): timeout
- plenti (oom): oom
- quarkdown (failed): SSGBERK_VERIFY_FAIL build exited 1
- quarto (oom): oom
- quartz (oom): oom
- rspress (failed): SSGBERK_VERIFY_FAIL build exited 1
- sculpin (oom): oom
- soupault (oom): oom
- sphinx (oom): oom
- starlight (failed): SSGBERK_VERIFY_FAIL build exited 134
- statiq (failed): SSGBERK_VERIFY_FAIL build exited 134
- sveltekit (oom): oom
- tableau (oom): oom
- tanstack-start (oom): oom
- vike (oom): oom
- vite-ssg (oom): oom
- vitepress (failed): SSGBERK_VERIFY_FAIL build exited 134
- vuepress (failed): SSGBERK_VERIFY_FAIL build exited 134
- zensical (timeout): timeout
- zine (oom): oom
