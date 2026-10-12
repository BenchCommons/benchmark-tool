# GitHub Actions ubuntu-24.04, one runner per generator

- Environment: GitHub Actions ubuntu-24.04, one runner per generator
- Started: 2026-10-11 06:46:05 UTC
- Completed: 2026-10-11 13:52:08 UTC
- Commit: 4c6e185b5b4a72c9779a722800b1133ff23bebdd

Suite: G v1 · cell 2/2 (nf 10000, cs 50) · profile core · resources 4 CPU / 8.0 GB

| Framework | Language | Files | Size (KB) | Min runs | Mean (s) | Stddev (s) | Median (s) | Min (s) | Max (s) | Status | Rank | CV | Posts/s | MB/s | CPU (cores) | Peak RSS (MB) | Output (MB / files) | Image build (s) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| jekyll | ruby | 10000 | 50 | 3 | 14.342 | 0.096 | 14.292 | 14.282 | 14.453 | ok | 1 | 0.7% | 699.7 | 36.0 | 1.00 | 1409.6 | 1100.8 / 10001 | 53.1 |
| zola | rust | 10000 | 50 | 3 | 15.327 | 1.069 | 14.804 | 14.620 | 16.556 | ok | 1 | 7.0% | 675.5 | 34.7 | 3.13 | 6068.1 | 877.6 / 10004 | 24.4 |
| bridgetown | ruby | 10000 | 50 | 3 | 19.845 | 0.943 | 20.243 | 18.768 | 20.524 | ok | 1 | 4.8% | 494.0 | 25.4 | 0.99 | 2854.3 | 991.5 / 10004 | 178.3 |
| metalsmith-handlebars | javascript | 10000 | 50 | 3 | 47.579 | 0.385 | 47.747 | 47.139 | 47.852 | ok | 1 | 0.8% | 209.4 | 10.8 | 1.12 | 2327.0 | 871.0 / 10002 | 36.3 |
| metalsmith-nunjucks | javascript | 10000 | 50 | 3 | 88.281 | 0.263 | 88.368 | 87.986 | 88.489 | ok | =2 | 0.3% | 113.2 | 5.8 | 1.10 | 2318.2 | 871.0 / 10002 | 33.1 |
| astro | javascript | 10000 | 50 | 3 | 88.332 | 1.699 | 87.953 | 86.855 | 90.189 | ok | =2 | 1.9% | 113.7 | 5.8 | 1.89 | 5758.4 | 1022.2 / 10001 | 45.6 |
| hugo | go | 10000 | 50 | 3 | 100.074 | 0.303 | 99.940 | 99.860 | 100.420 | ok | 4 | 0.3% | 100.1 | 5.1 | 3.79 | 7693.1 | 1143.7 / 10003 | 30.4 |
| nextjs-export | javascript | 10000 | 50 | 3 | 104.225 | 1.430 | 104.177 | 102.821 | 105.679 | ok | 2 | 1.4% | 96.0 | 4.9 | 1.92 | 1357.6 | 4921.4 / 50021 | 47.1 |
| nesta | ruby | 10000 | 50 | 3 | 119.060 | 1.398 | 119.490 | 117.498 | 120.192 | ok | 1 | 1.2% | 83.7 | 4.3 | 1.00 | 1397.3 | 846.1 / 10006 | 44.6 |
| cobalt | rust | 10000 | 50 | 3 | 154.302 | 0.056 | 154.325 | 154.238 | 154.342 | ok | 1 | 0.0% | 64.8 | 3.3 | 1.00 | 2636.8 | 806.4 / 10003 | 27.1 |
| publish | swift | 10000 | 50 | 3 | 210.416 | 0.372 | 210.480 | 210.016 | 210.751 | ok | 5 | 0.2% | 47.5 | 2.4 | 1.02 | 1405.2 | 784.0 / 10004 | 126.4 |
| jigsaw | php | 10000 | 50 | 3 | 238.222 | 0.222 | 238.211 | 238.005 | 238.449 | ok | 1 | 0.1% | 42.0 | 2.2 | 0.99 | 1152.2 | 846.2 / 10003 | 70.4 |
| sculpin | php | 10000 | 50 | 3 | 276.608 | 2.504 | 275.952 | 274.497 | 279.376 | ok | 2 | 0.9% | 36.2 | 1.9 | 1.00 | 5032.2 | 891.4 / 10003 | 71.9 |
| lektor | python | 10000 | 50 | 3 | 428.248 | 10.895 | 429.880 | 416.629 | 438.234 | ok | 1 | 2.5% | 23.3 | 1.2 | 0.98 | 772.2 | 811.2 / 10004 | 50.2 |
| lustre-ssg | gleam | 10000 | 50 | 3 | 441.453 | 4.570 | 439.031 | 438.604 | 446.724 | ok | 1 | 1.0% | 22.8 | 1.2 | 1.30 | 2117.5 | 829.4 / 10004 | 24.9 |
| middleman | ruby | 10000 | 50 | 3 | 513.949 | 1.813 | 514.924 | 511.858 | 515.066 | ok | 6 | 0.4% | 19.4 | 1.0 | 3.80 | 853.5 | 980.4 / 10002 | 105.2 |
| nanoc | ruby | 10000 | 50 | 3 | 531.574 | 11.099 | 530.778 | 520.895 | 543.050 | ok | 3 | 2.1% | 18.8 | 1.0 | 1.00 | 3489.4 | 981.0 / 10001 | 43.4 |
| tableau | elixir | 10000 | 50 | 3 | 592.328 | 1.197 | 591.956 | 591.360 | 593.667 | ok | 2 | 0.2% | 16.9 | 0.9 | 2.82 | 3411.5 | 891.6 / 10004 | 78.3 |
| jbake | java | 10000 | 50 | 3 | 639.030 | 10.329 | 634.867 | 631.432 | 650.792 | ok | 3 | 1.6% | 15.8 | 0.8 | 1.17 | 4110.2 | 831.6 / 10003 | 41.9 |
| pelican | python | 10000 | 50 | 3 | 706.156 | 4.917 | 704.811 | 702.051 | 711.605 | ok | 7 | 0.7% | 14.2 | 0.7 | 1.00 | 790.4 | 722.4 / 10001 | 46.4 |
| hakyll | haskell | 10000 | 50 | 3 | 712.890 | 0.751 | 712.828 | 712.172 | 713.671 | ok | 1 | 0.1% | 14.0 | 0.7 | 3.45 | 2715.4 | 963.4 / 10003 | 1972.1 |
| mkdocs | python | 10000 | 50 | 3 | 861.949 | 37.051 | 848.288 | 833.668 | 903.890 | ok | 2 | 4.3% | 11.8 | 0.6 | 1.00 | 2552.8 | 884.2 / 10001 | 44.3 |
| franklin | julia | 10000 | 50 | 3 | 938.246 | 5.867 | 941.351 | 931.479 | 941.910 | ok | 4 | 0.6% | 10.6 | 0.5 | 1.00 | 5677.8 | 1087.2 / 10005 | 238.2 |
| antora | javascript | 10000 | 50 | 3 | 1063.355 | 27.366 | 1065.845 | 1034.829 | 1089.390 | ok | 4 | 2.6% | 9.4 | 0.5 | 1.09 | 3610.1 | 1937.9 / 10003 | 38.8 |
| cecil | php | 10000 | 50 | 3 | 1131.197 | 33.167 | 1118.473 | 1106.275 | 1168.842 | ok | =8 | 2.9% | 8.9 | 0.5 | 1.00 | 2406.7 | 859.6 / 10004 | 57.8 |
| docfx | c# | 10000 | 50 | 3 | 1160.927 | 13.544 | 1161.752 | 1146.989 | 1174.040 | ok | =8 | 1.2% | 8.6 | 0.4 | 1.65 | 6548.4 | 884.9 / 10006 | 48.8 |
| nikola-mako | python | 10000 | 50 | 3 | 1733.111 | 14.176 | 1730.766 | 1720.254 | 1748.314 | ok | 10 | 0.8% | 5.8 | 0.3 | 1.00 | 448.1 | 837.8 / 10025 | 57.0 |
| gatsby | javascript | 10000 | 50 | 3 | 1946.958 | 20.200 | 1938.542 | 1932.326 | 1970.005 | ok | 11 | 1.0% | 5.2 | 0.3 | 1.32 | 4094.3 | 1702.7 / 20030 | 236.0 |
| analog | javascript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 61.3 |
| cryogen | clojure | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 47.4 |
| docmd | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 38.7 |
| docusaurus | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 106.7 |
| dumi | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 77.7 |
| eleventy | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 37.3 |
| emanote | haskell | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 3375.0 |
| hexo | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 41.5 |
| iles | javascript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 44.5 |
| ink | go | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 74.7 |
| laika | scala | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 41.4 |
| lume | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 33.1 |
| marmite | rust | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 45.8 |
| mdbook | rust | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 27.0 |
| nextra | javascript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 75.3 |
| nimib | nim | 10000 | 50 | — | — | — | — | — | — | timeout | — | — | — | — | — | — | — | 55.3 |
| nuxt-content | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 55.9 |
| observable-framework | javascript | 10000 | 50 | — | — | — | — | — | — | timeout | — | — | — | — | — | — | — | 42.7 |
| plenti | go | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 87.7 |
| quarkdown | kotlin | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 35.3 |
| quarto | typescript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 34.0 |
| quartz | javascript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 269.9 |
| rspress | javascript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 45.5 |
| soupault | ocaml | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 30.5 |
| sphinx | python | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 50.4 |
| starlight | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 50.8 |
| statiq | c# | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 60.1 |
| sveltekit | javascript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 39.3 |
| tanstack-start | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 45.3 |
| vike | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 44.7 |
| vite-ssg | javascript | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 37.7 |
| vitepress | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 40.0 |
| vuepress | javascript | 10000 | 50 | — | — | — | — | — | — | failed | — | — | — | — | — | — | — | 37.4 |
| zensical | python | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 55.1 |
| zine | zig | 10000 | 50 | — | — | — | — | — | — | oom | — | — | — | — | — | — | — | 28.2 |

## Ranking

Ordered by median; generators whose min–max ranges overlap share a rank (`=n`). Only results of the same suite, cell, profile, fingerprint and feature set are ranked together.

### G v1 · nf 10000, cs 50 · profile core · fingerprint 3f2f1aaf006c

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | jekyll | 14.292 | 0.7% | 14.282–14.453 |
| =2 | astro | 87.953 | 1.9% | 86.855–90.189 |
| =2 | metalsmith-nunjucks | 88.368 | 0.3% | 87.986–88.489 |
| 4 | hugo | 99.940 | 0.3% | 99.860–100.420 |
| 5 | publish | 210.480 | 0.2% | 210.016–210.751 |
| 6 | middleman | 514.924 | 0.4% | 511.858–515.066 |
| 7 | pelican | 704.811 | 0.7% | 702.051–711.605 |
| =8 | cecil | 1118.473 | 2.9% | 1106.275–1168.842 |
| =8 | docfx | 1161.752 | 1.2% | 1146.989–1174.040 |
| 10 | nikola-mako | 1730.766 | 0.8% | 1720.254–1748.314 |
| 11 | gatsby | 1938.542 | 1.0% | 1932.326–1970.005 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint ebe58c534103

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | zola | 14.804 | 7.0% | 14.620–16.556 |
| 2 | nextjs-export | 104.177 | 1.4% | 102.821–105.679 |
| 3 | nanoc | 530.778 | 2.1% | 520.895–543.050 |
| 4 | antora | 1065.845 | 2.6% | 1034.829–1089.390 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint 90616b2b906d

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | bridgetown | 20.243 | 4.8% | 18.768–20.524 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint dc6727d97293

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | metalsmith-handlebars | 47.747 | 0.8% | 47.139–47.852 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint de731ab3b8a5

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | nesta | 119.490 | 1.2% | 117.498–120.192 |
| 2 | tableau | 591.956 | 0.2% | 591.360–593.667 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint ae30efe0efb4

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | cobalt | 154.325 | 0.0% | 154.238–154.342 |
| 2 | sculpin | 275.952 | 0.9% | 274.497–279.376 |
| 3 | jbake | 634.867 | 1.6% | 631.432–650.792 |
| 4 | franklin | 941.351 | 0.6% | 931.479–941.910 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint 2f62636d600c

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | jigsaw | 238.211 | 0.1% | 238.005–238.449 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint 2bb7b205c77e

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | lektor | 429.880 | 2.5% | 416.629–438.234 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint ba134637a49c

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | lustre-ssg | 439.031 | 1.0% | 438.604–446.724 |

### G v1 · nf 10000, cs 50 · profile core · fingerprint 8e17af3b158e

| Rank | Framework | Median (s) | CV | Min–Max (s) |
|---|---|---|---|---|
| 1 | hakyll | 712.828 | 0.1% | 712.172–713.671 |
| 2 | mkdocs | 848.288 | 4.3% | 833.668–903.890 |

## Caveats

- T9: oom means the generator exceeded the container memory limit, which is the same for every generator; it is an outcome, not a time.
- T7: peak RSS is the largest single process, not the sum, so it under-reports multi-process generators.

## Failed / timeout / oom / nonconformant / unsupported

- analog (oom): oom
- cryogen (failed): SSGBERK_VERIFY_FAIL expected=10000 got=0
- docmd (failed): SSGBERK_VERIFY_FAIL build exited 134
- docusaurus (failed): SSGBERK_VERIFY_FAIL build exited 134
- dumi (failed): SSGBERK_VERIFY_FAIL build exited 134
- eleventy (failed): SSGBERK_VERIFY_FAIL build exited 134
- emanote (oom): oom
- hexo (failed): SSGBERK_VERIFY_FAIL build exited 134
- iles (oom): oom
- ink (oom): oom
- laika (failed): SSGBERK_VERIFY_FAIL build exited 1
- lume (failed): SSGBERK_VERIFY_FAIL build exited 133
- marmite (oom): oom
- mdbook (oom): oom
- nextra (oom): oom
- nimib (timeout): timeout
- nuxt-content (failed): SSGBERK_VERIFY_FAIL build exited 1
- observable-framework (timeout): timeout
- plenti (failed): SSGBERK_VERIFY_FAIL build exited 2
- quarkdown (failed): SSGBERK_VERIFY_FAIL build exited 1
- quarto (oom): oom
- quartz (oom): oom
- rspress (oom): oom
- soupault (oom): oom
- sphinx (oom): oom
- starlight (failed): SSGBERK_VERIFY_FAIL build exited 134
- statiq (failed): SSGBERK_VERIFY_FAIL build exited 134
- sveltekit (oom): oom
- tanstack-start (failed): SSGBERK_VERIFY_FAIL build exited 1
- vike (failed): SSGBERK_VERIFY_FAIL build exited 1
- vite-ssg (oom): oom
- vitepress (failed): SSGBERK_VERIFY_FAIL build exited 134
- vuepress (failed): SSGBERK_VERIFY_FAIL build exited 134
- zensical (oom): oom
- zine (oom): oom
