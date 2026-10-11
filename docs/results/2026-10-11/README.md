# Benchmark rounds 2026-10-11: suites P and M, 63 generators

All 63 generators of ssg-frameworks on GitHub Actions (`ubuntu-24.04` hosted runners, one runner per generator and cell, `--cpus 4 --memory 8g`, profile `core`, Node generators with `--max-old-space-size=6144`). Suite P also ran the untimed output quality pass (spec 009) in cell nf50-cs5.

| Suite | Pages | Sizes | Workflow run | Files |
|---|---|---|---|---|
| P (website pessoal) | 50 | 5 KB, 50 KB | [38102505695](https://github.com/BenchCommons/benchmark-tool/actions/runs/38102505695) | [P/](./P/) |
| M (site corporativo) | 1,000 | 5 KB, 50 KB | [38102507250](https://github.com/BenchCommons/benchmark-tool/actions/runs/38102507250) | [M/](./M/) |

## Caveats

- **Rankings are per runner.** Hosted runners differ in CPU model, so the per-cell `summary.md` ranks only generators that shared a runner fingerprint. The tables below show medians side by side for reading.
- **heap** means the generator aborted at its runtime heap cap (exit 134: the 6 GB V8 heap, or the .NET runtime); **oom** means the kernel killed it at the 8 GB container limit.
- **Quality** results are in `P/nf50-cs5/quality-summary.csv` and in `quality` of `P/nf50-cs5/results.json`. Only 15 generators render the SF 005 index layout; for the others the audited post page is the first file matching `output_glob` (`postSource: glob`).

## P: 50 pages

### 50 pages × 5 KB (62/63 ok)

| Generator | Language | Median (s) | CV | Posts/s | Peak RSS (MB) |
|---|---|---|---|---|---|
| zola | rust | 0.020 | 4.2% | 2,445 | 34 |
| zine | zig | 0.024 | 2.0% | 2,053 | 17 |
| cobalt | rust | 0.028 | 1.3% | 1,793 | 12 |
| mdbook | rust | 0.039 | 1.7% | 1,266 | 17 |
| ink | go | 0.068 | 1.6% | 739 | 21 |
| hugo | go | 0.070 | 1.4% | 711 | 87 |
| publish | swift | 0.107 | 4.5% | 467 | 30 |
| metalsmith-nunjucks | javascript | 0.198 | 2.5% | 253 | 87 |
| marmite | rust | 0.203 | 1.5% | 247 | 179 |
| metalsmith-handlebars | javascript | 0.227 | 3.2% | 221 | 92 |
| jigsaw | php | 0.251 | 0.5% | 199 | 41 |
| nimib | nim | 0.279 | 0.5% | 179 | 5 |
| soupault | ocaml | 0.313 | 0.8% | 160 | 39 |
| cecil | php | 0.330 | 1.4% | 152 | 57 |
| sculpin | php | 0.342 | 0.6% | 146 | 57 |
| lume | javascript | 0.488 | 2.2% | 102 | 131 |
| lustre-ssg | gleam | 0.510 | 1.9% | 98 | 78 |
| mkdocs | python | 0.511 | 0.9% | 98 | 33 |
| nesta | ruby | 0.539 | 1.9% | 93 | 64 |
| eleventy | javascript | 0.617 | 0.7% | 81 | 136 |
| pelican | python | 0.640 | 1.2% | 78 | 42 |
| lektor | python | 0.654 | 0.6% | 77 | 50 |
| hexo | javascript | 0.999 | 0.8% | 50 | 150 |
| docmd | javascript | 1.117 | 1.0% | 45 | 139 |
| vike | javascript | 1.121 | 0.7% | 45 | 411 |
| hakyll | haskell | 1.124 | 1.2% | 44 | 314 |
| nanoc | ruby | 1.180 | 1.1% | 42 | 75 |
| zensical | python | 1.194 | 0.5% | 42 | 70 |
| jekyll | ruby | 1.295 | 2.7% | 39 | 81 |
| bridgetown | ruby | 1.333 | 0.2% | 38 | 81 |
| tableau | elixir | 1.621 | 2.4% | 31 | 239 |
| vuepress | javascript | 1.650 | 1.9% | 30 | 500 |
| middleman | ruby | 1.720 | 0.7% | 29 | 97 |
| tanstack-start | javascript | 1.757 | 4.1% | 28 | 428 |
| docfx | c# | 1.773 | 3.3% | 28 | 136 |
| laika | scala | 1.792 | 4.0% | 28 | 288 |
| quarkdown | kotlin | 1.930 | 1.4% | 26 | 202 |
| astro | javascript | 2.094 | 1.3% | 24 | 615 |
| iles | javascript | 2.172 | 1.0% | 23 | 702 |
| plenti | go | 2.442 | 3.7% | 20 | 168 |
| antora | javascript | 2.734 | 2.5% | 18 | 223 |
| vitepress | javascript | 2.774 | 0.3% | 18 | 455 |
| quartz | javascript | 2.878 | 0.9% | 17 | 453 |
| sveltekit | javascript | 2.931 | 2.5% | 17 | 723 |
| vite-ssg | javascript | 3.026 | 0.7% | 17 | 687 |
| starlight | javascript | 3.047 | 3.2% | 16 | 822 |
| franklin | julia | 3.064 | 2.9% | 16 | 491 |
| rspress | javascript | 3.132 | 4.7% | 16 | 890 |
| emanote | haskell | 3.340 | 3.9% | 15 | 178 |
| sphinx | python | 3.663 | 0.8% | 14 | 102 |
| jbake | java | 4.603 | 0.8% | 11 | 438 |
| nextjs-export | javascript | 4.869 | 0.3% | 10 | 1,403 |
| nikola-mako | python | 5.043 | 0.3% | 10 | 62 |
| analog | javascript | 5.135 | 0.5% | 10 | 1,650 |
| cryogen | clojure | 5.628 | 3.5% | 9 | 629 |
| observable-framework | javascript | 5.660 | 0.4% | 9 | 591 |
| nuxt-content | javascript | 7.736 | 0.4% | 6 | 1,124 |
| statiq | c# | 14.335 | 5.9% | 3 | 492 |
| gatsby | javascript | 21.090 | 1.2% | 2 | 683 |
| docusaurus | javascript | 26.857 | 1.3% | 2 | 1,870 |
| nextra | javascript | 27.504 | 1.1% | 2 | 1,674 |
| quarto | typescript | 40.237 | 0.4% | 1 | 415 |

Failed: dumi: no result, the job failed before uploading.

### 50 pages × 50 KB (63/63 ok)

| Generator | Language | Median (s) | CV | Posts/s | Peak RSS (MB) |
|---|---|---|---|---|---|
| zine | zig | 0.117 | 1.1% | 428 | 117 |
| cobalt | rust | 0.151 | 1.1% | 331 | 23 |
| zola | rust | 0.158 | 1.0% | 316 | 68 |
| mdbook | rust | 0.212 | 1.5% | 236 | 84 |
| hugo | go | 0.396 | 1.9% | 126 | 273 |
| metalsmith-nunjucks | javascript | 0.541 | 4.9% | 92 | 124 |
| marmite | rust | 0.713 | 0.8% | 70 | 1,389 |
| metalsmith-handlebars | javascript | 0.726 | 1.1% | 69 | 125 |
| publish | swift | 0.996 | 0.5% | 50 | 35 |
| nesta | ruby | 1.067 | 0.8% | 47 | 80 |
| eleventy | javascript | 1.199 | 1.2% | 42 | 297 |
| jigsaw | php | 1.345 | 1.0% | 37 | 47 |
| sculpin | php | 1.445 | 0.3% | 35 | 78 |
| soupault | ocaml | 1.560 | 1.9% | 32 | 185 |
| tanstack-start | javascript | 1.601 | 2.6% | 31 | 546 |
| vike | javascript | 1.672 | 1.1% | 30 | 535 |
| lume | javascript | 1.697 | 4.2% | 29 | 256 |
| nimib | nim | 1.697 | 1.2% | 29 | 10 |
| tableau | elixir | 1.730 | 2.2% | 29 | 272 |
| cecil | php | 1.844 | 0.6% | 27 | 67 |
| hexo | javascript | 2.030 | 2.6% | 25 | 438 |
| middleman | ruby | 2.436 | 0.9% | 21 | 100 |
| nanoc | ruby | 2.535 | 6.4% | 20 | 109 |
| astro | javascript | 2.619 | 0.9% | 19 | 894 |
| lustre-ssg | gleam | 2.624 | 1.8% | 19 | 101 |
| lektor | python | 3.168 | 1.2% | 16 | 57 |
| vuepress | javascript | 3.264 | 3.6% | 15 | 1,240 |
| pelican | python | 3.693 | 0.3% | 14 | 46 |
| docmd | javascript | 3.820 | 0.7% | 13 | 337 |
| jekyll | ruby | 3.928 | 0.8% | 13 | 111 |
| hakyll | haskell | 4.036 | 1.6% | 12 | 818 |
| quarkdown | kotlin | 4.100 | 5.1% | 12 | 335 |
| plenti | go | 4.408 | 0.7% | 11 | 386 |
| jbake | java | 4.738 | 4.2% | 11 | 553 |
| bridgetown | ruby | 4.918 | 0.9% | 10 | 105 |
| starlight | javascript | 5.060 | 0.3% | 10 | 1,355 |
| mkdocs | python | 5.143 | 1.1% | 10 | 55 |
| laika | scala | 6.236 | 5.1% | 8 | 912 |
| nextjs-export | javascript | 6.566 | 1.4% | 8 | 1,414 |
| franklin | julia | 7.463 | 0.7% | 7 | 517 |
| vitepress | javascript | 7.543 | 1.9% | 7 | 1,066 |
| docfx | c# | 8.186 | 0.9% | 6 | 241 |
| analog | javascript | 8.401 | 0.5% | 6 | 1,933 |
| quartz | javascript | 10.286 | 2.2% | 5 | 968 |
| vite-ssg | javascript | 10.325 | 0.8% | 5 | 2,194 |
| nikola-mako | python | 12.596 | 0.4% | 4 | 68 |
| antora | javascript | 13.698 | 0.5% | 4 | 457 |
| zensical | python | 15.782 | 0.3% | 3 | 141 |
| nuxt-content | javascript | 16.454 | 1.3% | 3 | 1,603 |
| cryogen | clojure | 17.192 | 1.1% | 3 | 2,144 |
| ink | go | 17.287 | 0.1% | 3 | 82 |
| iles | javascript | 18.975 | 2.4% | 3 | 1,035 |
| emanote | haskell | 18.990 | 1.1% | 3 | 431 |
| sveltekit | javascript | 19.314 | 0.4% | 3 | 982 |
| statiq | c# | 24.105 | 4.5% | 2 | 1,448 |
| observable-framework | javascript | 24.491 | 1.1% | 2 | 817 |
| rspress | javascript | 26.235 | 1.2% | 2 | 2,862 |
| sphinx | python | 27.053 | 1.3% | 2 | 436 |
| gatsby | javascript | 32.515 | 1.5% | 2 | 833 |
| nextra | javascript | 55.001 | 1.5% | 1 | 3,008 |
| quarto | typescript | 125.470 | 1.4% | 0 | 957 |
| docusaurus | javascript | 125.939 | 0.5% | 0 | 4,150 |
| dumi | javascript | 133.878 | 0.8% | 0 | 3,510 |

## M: 1,000 pages

### 1,000 pages × 5 KB (63/63 ok)

| Generator | Language | Median (s) | CV | Posts/s | Peak RSS (MB) |
|---|---|---|---|---|---|
| zola | rust | 0.282 | 0.6% | 3,543 | 103 |
| zine | zig | 0.329 | 0.7% | 3,037 | 233 |
| hugo | go | 0.675 | 1.5% | 1,483 | 483 |
| metalsmith-handlebars | javascript | 0.905 | 2.7% | 1,105 | 207 |
| ink | go | 0.994 | 0.8% | 1,006 | 137 |
| cobalt | rust | 1.222 | 0.7% | 818 | 55 |
| metalsmith-nunjucks | javascript | 1.683 | 1.8% | 594 | 211 |
| eleventy | javascript | 1.688 | 2.4% | 592 | 337 |
| jekyll | ruby | 1.831 | 0.9% | 546 | 105 |
| lume | javascript | 1.874 | 2.4% | 534 | 284 |
| publish | swift | 2.546 | 0.4% | 393 | 54 |
| jigsaw | php | 2.888 | 0.3% | 346 | 75 |
| mdbook | rust | 3.651 | 0.6% | 274 | 170 |
| marmite | rust | 3.670 | 5.6% | 272 | 3,070 |
| bridgetown | ruby | 3.811 | 0.9% | 262 | 129 |
| astro | javascript | 4.024 | 3.6% | 249 | 810 |
| cecil | php | 4.218 | 0.3% | 237 | 95 |
| hexo | javascript | 4.350 | 2.3% | 230 | 720 |
| sculpin | php | 4.531 | 0.5% | 221 | 156 |
| tanstack-start | javascript | 4.662 | 1.3% | 214 | 669 |
| soupault | ocaml | 4.699 | 0.3% | 213 | 408 |
| vike | javascript | 4.786 | 0.9% | 209 | 839 |
| middleman | ruby | 5.205 | 0.9% | 192 | 124 |
| lustre-ssg | gleam | 5.591 | 1.3% | 179 | 151 |
| docfx | c# | 5.646 | 3.9% | 177 | 220 |
| quarkdown | kotlin | 6.057 | 1.5% | 165 | 489 |
| lektor | python | 7.275 | 4.6% | 137 | 73 |
| nesta | ruby | 7.628 | 2.0% | 131 | 87 |
| pelican | python | 8.260 | 0.2% | 121 | 51 |
| tableau | elixir | 8.371 | 1.1% | 119 | 428 |
| franklin | julia | 8.744 | 7.9% | 114 | 610 |
| starlight | javascript | 8.991 | 1.3% | 111 | 1,104 |
| vuepress | javascript | 10.234 | 4.9% | 98 | 2,123 |
| nanoc | ruby | 10.585 | 1.5% | 94 | 155 |
| mkdocs | python | 10.928 | 0.5% | 92 | 59 |
| nextjs-export | javascript | 11.094 | 0.9% | 90 | 1,396 |
| laika | scala | 11.297 | 4.8% | 89 | 1,287 |
| hakyll | haskell | 11.411 | 0.8% | 88 | 548 |
| quartz | javascript | 14.173 | 1.2% | 71 | 2,473 |
| statiq | c# | 14.436 | 6.0% | 69 | 1,438 |
| jbake | java | 15.371 | 2.8% | 65 | 677 |
| docmd | javascript | 15.716 | 0.6% | 64 | 813 |
| vitepress | javascript | 17.122 | 1.6% | 58 | 1,826 |
| cryogen | clojure | 17.219 | 3.3% | 58 | 1,754 |
| antora | javascript | 18.466 | 1.6% | 54 | 544 |
| nikola-mako | python | 19.346 | 2.7% | 52 | 101 |
| plenti | go | 19.872 | 0.7% | 50 | 1,520 |
| vite-ssg | javascript | 21.958 | 3.5% | 46 | 5,304 |
| analog | javascript | 22.673 | 1.3% | 44 | 2,266 |
| emanote | haskell | 26.757 | 4.3% | 37 | 725 |
| nimib | nim | 27.845 | 0.6% | 36 | 7 |
| zensical | python | 33.447 | 0.7% | 30 | 219 |
| gatsby | javascript | 35.313 | 0.6% | 28 | 785 |
| nuxt-content | javascript | 38.025 | 5.2% | 26 | 1,814 |
| iles | javascript | 40.288 | 2.2% | 25 | 1,556 |
| sveltekit | javascript | 42.909 | 0.5% | 23 | 1,408 |
| rspress | javascript | 52.150 | 1.9% | 19 | 5,439 |
| sphinx | python | 72.227 | 1.2% | 14 | 761 |
| nextra | javascript | 95.141 | 1.6% | 11 | 6,214 |
| observable-framework | javascript | 121.119 | 1.0% | 8 | 1,663 |
| docusaurus | javascript | 254.101 | 1.5% | 4 | 6,411 |
| dumi | javascript | 669.898 | 0.4% | 1 | 4,868 |
| quarto | typescript | 775.782 | 0.4% | 1 | 907 |

### 1,000 pages × 50 KB (53/63 ok)

| Generator | Language | Median (s) | CV | Posts/s | Peak RSS (MB) |
|---|---|---|---|---|---|
| zola | rust | 2.590 | 8.4% | 386 | 643 |
| zine | zig | 3.132 | 0.9% | 319 | 2,219 |
| cobalt | rust | 3.633 | 0.2% | 275 | 272 |
| jekyll | ruby | 5.077 | 0.8% | 197 | 271 |
| bridgetown | ruby | 6.173 | 2.2% | 162 | 370 |
| metalsmith-nunjucks | javascript | 6.769 | 1.6% | 148 | 546 |
| mdbook | rust | 7.192 | 0.4% | 139 | 1,506 |
| eleventy | javascript | 9.060 | 1.6% | 110 | 1,120 |
| metalsmith-handlebars | javascript | 9.537 | 1.4% | 105 | 568 |
| astro | javascript | 9.780 | 1.2% | 102 | 1,351 |
| hugo | go | 9.793 | 0.9% | 102 | 3,897 |
| nesta | ruby | 10.394 | 1.0% | 96 | 210 |
| publish | swift | 11.443 | 2.0% | 87 | 161 |
| tanstack-start | javascript | 14.175 | 0.5% | 71 | 1,627 |
| vike | javascript | 14.796 | 1.1% | 68 | 2,486 |
| tableau | elixir | 15.779 | 0.3% | 63 | 542 |
| nextjs-export | javascript | 17.665 | 1.5% | 57 | 1,411 |
| quarkdown | kotlin | 17.864 | 1.9% | 56 | 2,136 |
| hexo | javascript | 22.481 | 1.6% | 44 | 3,420 |
| lume | javascript | 23.543 | 1.7% | 42 | 1,689 |
| sculpin | php | 23.812 | 0.2% | 42 | 554 |
| jigsaw | php | 25.889 | 0.3% | 39 | 152 |
| jbake | java | 28.510 | 2.1% | 35 | 1,355 |
| cecil | php | 33.690 | 0.3% | 30 | 290 |
| starlight | javascript | 34.544 | 0.6% | 29 | 2,477 |
| pelican | python | 36.256 | 1.0% | 28 | 117 |
| lustre-ssg | gleam | 41.898 | 1.0% | 24 | 286 |
| soupault | ocaml | 42.083 | 0.5% | 24 | 3,372 |
| middleman | ruby | 46.146 | 0.9% | 22 | 186 |
| laika | scala | 53.312 | 4.8% | 19 | 3,923 |
| nanoc | ruby | 60.397 | 2.4% | 17 | 481 |
| lektor | python | 60.841 | 1.2% | 16 | 153 |
| docmd | javascript | 67.145 | 0.3% | 15 | 1,946 |
| docfx | c# | 75.420 | 2.1% | 13 | 882 |
| hakyll | haskell | 86.405 | 0.8% | 12 | 2,565 |
| nimib | nim | 91.668 | 1.1% | 11 | 12 |
| franklin | julia | 94.464 | 0.3% | 11 | 1,066 |
| mkdocs | python | 104.730 | 1.2% | 10 | 287 |
| analog | javascript | 106.359 | 0.5% | 9 | 4,838 |
| vuepress | javascript | 108.790 | 28.5% | 9 | 8,327 |
| nikola-mako | python | 125.674 | 0.8% | 8 | 102 |
| plenti | go | 152.053 | 0.4% | 7 | 2,254 |
| cryogen | clojure | 193.944 | 1.6% | 5 | 2,500 |
| antora | javascript | 223.601 | 0.9% | 4 | 895 |
| gatsby | javascript | 234.610 | 0.9% | 4 | 1,151 |
| iles | javascript | 250.694 | 4.9% | 4 | 6,053 |
| ink | go | 273.979 | 0.1% | 4 | 1,365 |
| zensical | python | 308.209 | 0.1% | 3 | 1,334 |
| nuxt-content | javascript | 355.651 | 2.4% | 3 | 5,914 |
| emanote | haskell | 437.994 | 0.5% | 2 | 5,883 |
| observable-framework | javascript | 464.846 | 2.0% | 2 | 1,276 |
| sveltekit | javascript | 469.664 | 1.3% | 2 | 4,627 |
| sphinx | python | 751.941 | 1.2% | 1 | 7,212 |

Failed: docusaurus: heap (exit 134); dumi: heap (exit 134); marmite: oom (8 GB container); nextra: oom (8 GB container); quarto: timeout; quartz: oom (8 GB container); rspress: oom (8 GB container); statiq: heap (exit 134); vite-ssg: oom (8 GB container); vitepress: heap (exit 134).
