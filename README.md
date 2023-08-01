# quarto-manuscripts

Slides and materials for the "Reproducible Manuscripts with Quarto" talk at posit::conf(2023).

## Video 1: Getting started with Quarto manuscripts

<https://rstudio.wistia.com/medias/lxzxu9wuyq>

```
<script src="https://fast.wistia.com/embed/medias/lxzxu9wuyq.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:56.25% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_lxzxu9wuyq seo=true videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/lxzxu9wuyq/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>
```

- RStudio > File > New Project > New Directory > Quarto Manuscript
- In the Quarto Manuscript dialogue:
  - Directory name: `la-palma-earthquakes`
  - Check: Create a git repository
- In `index.qmd` in the new project:
  - Update `title`: 
  ```
  La Palma Earthquakes
  ```
  - Update `authors`:
  ```
  - name: Steve Purves
    orcid: 0000-0002-0760-5497
    corresponding: true
    email: steve@curvenote.com
    roles:
      - Investigation
      - Project administration
      - Software
      - Visualization
    affiliations:
      - Curvenote
  - name: Rowan Cockett
    orcid: 0000-0002-7859-8394
    corresponding: false
    roles: []
    affiliations:
      - Curvenote
  ```
  - Update `keywords`:
  ```
  keywords:
  - La Palma
  - Earthquakes
  ```
- Render, pop out to new browser window
- Run `use_git()` and then `usethis::use_github()`
- In the Terminal, publish to GitHub Pages
- Once published, show how Hypothesis works

## Video 2: Multiple formats

https://rstudio.wistia.com/medias/rjpyfnto0o

```
<script src="https://fast.wistia.com/embed/medias/rjpyfnto0o.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:56.25% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_rjpyfnto0o seo=true videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/rjpyfnto0o/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>
```

- Show the MS Word output by downloading, then navigate in the Finder to the `_manuscript` folder
- In `_quarto.yml` under `formats` 
```
pdf: true
```
- Install `agu` extension in the Terminal:
```
quarto add quarto-journals/agu
```
- In `_quarto.yml` and under `formats`, make `pdf` into
```
agu-pdf: default
```
- Re-render and show that PDF is styled for AGU journal
- Install `plos` extension in the Terminal:
```
quarto add quarto-journals/plos
```
- In `_quarto.yml` and under `formats`, change journal to PLOS
```
plos-pdf: default
```
- Re-render and show that PDF is now styled for PLOS journal
- Add `keep-tex` to `plos-pdf`:
```
plos-pdf:
  keep-tex: true 
```
- Re-render and show that in the Finder, in project folder root, there is now a `index.tex` file. Open it, and highlight the `\documentclass[10pt, letterpaper]{article}` lines

## Video 3: MECA bundle

<https://rstudio.wistia.com/medias/cnzvad8r1d>

```
<script src="https://fast.wistia.com/embed/medias/cnzvad8r1d.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:56.25% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_cnzvad8r1d seo=true videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/cnzvad8r1d/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>
```

- Terminal: `quarto render` (or Build Tab > Render Project)
- Show the MECA bundle output in the Finder in `_manuscript` folder

## Video 4: Front matter

- Add `agu-pdf` back to `_quarto.yml`
```
agu-pdf: default
```
- Add more to `index.qmd` YAML
```
abstract: |
  In September 2021, a significant jump in seismic activity on the island of La Palma (Canary Islands, Spain) signaled the start of a volcanic crisis that still continues at the time of writing. Earthquake data is continually collected and published by the Instituto Geográphico Nacional (IGN). ...
plain-language-summary: |
  Earthquake data for the island of La Palma from the September 2021 eruption is found ...
key-points:
  - A web scraping script was developed to pull data from the Instituto Geogràphico Nacional into a machine-readable form for analysis
  - Earthquake events on La Palma are consistent with the presence of both mantle and crustal reservoirs.
date: last-modified
number-sections: true
```
- Re-render and show that some of these show up on the HTML and some on the AGU PDF and some on the PLOS PDF output

## Video 4: Add content

Start with the following code chunks in the document:

```{r}
#| label: load-pkgs

library(tidyverse)
```

```{r}
#| label: eruptions

eruptions <- tibble(
  year = c(1492, 1585, 1646, 1677, 1712, 1949, 1971, 2021)
)
n_eruptions <- nrow(eruptions)
```

```{r}
#| label: avg-yrs-between-eruptions

avg_years_between_eruptions <- eruptions |>
  filter(year != 2021) |>
  mutate(
    year_lag = lag(year),
    diff = year - year_lag
  ) |>
  summarize(avg_diff = mean(diff, na.rm = TRUE)) |>
  pull()
```

- Add the following text:

```
Based on data up to and including 1971, eruptions on La Palma happen every `r round(avg_years_between_eruptions, 1)` years on average.
```

- Add the following text:

```
Studies of the magma systems feeding the volcano, such as ___, have proposed that there are two main magma reservoirs feeding the Cumbre Vieja volcano; one in the mantle (30-40km depth) which charges and in turn feeds a shallower crustal reservoir (10-20km depth).
```

- Add citation for DOI: 10.1186/s13617-019-0085-5

- Add the following chunk:

```{r}
#| label: fig-timeline
#| fig-cap: Timeline of recent eruptions on La Palma
#| fig-alt: An event plot of the years of the last 8 eruptions on La Palma.
#| fig-height: 1.5
#| fig-width: 6

ggplot(eruptions, aes(x = year, y = 0)) +
  geom_text(label = "|") +
  theme_minimal() +
  labs(y = NULL) +
  theme(
    panel.grid = element_blank(),
    axis.text.y = element_blank()
  )
```

- Add cross ref to `@fig-timeline`:

```
Eight eruptions have been recorded since the late 1400s (@fig-timeline).
```

- Add 2nd level heading, and label it `{#sec-data-methods}`

```
## Data & Methods
```

- Add crossref to this heading

```
Data and methods are discussed in @sec-data-methods.
```

- Add equation

```
Let $x$ denote the number of eruptions in a year. Then, $x$ can be modeled by a Poisson distribution

$$
p(x) = \frac{e^{-\lambda} \lambda^{x}}{x !}
$$ {#eq-poisson}

where $\lambda$ is the rate of eruptions per year. Using @eq-poisson, the probability of an eruption in the next $t$ years can be calculated.
```

- Insert table with caption and ID

```
| Name                | Year |
|---------------------|------|
| Current             | 2021 |
| Teneguía            | 1971 |
| Nambroque           | 1949 |
| El Charco           | 1712 |
| Volcán San Antonio  | 1677 |
| Volcán San Martin   | 1646 |
| Tajuya near El Paso | 1585 |
| Montaña Quemada     | 1492 |

: Recent historic eruptions on La Palma {#tbl-history}
```

- Add crossref to table

```
@tbl-history summarizes the eruptions recorded since the colonization of the islands by Europeans in the late 1400s.
```

- Add image and crossref to it

```
La Palma is one of the west most islands in the Volcanic Archipelago of the Canary Islands (@fig-map).

![Map of La Palma](images/la-palma-map.png){#fig-map}
```

## Video 5: Embed computing

- Add a `.qmd` and a `.ipynb` with computation
- Commit and push everything
- Embed results from the`.qmd`

```
{{< embed notebooks/explore-earthquakes.qmd#tbl-yearly-earthquakes >}}

@tbl-yearly-earthquakes shows the yearly number of earthquakes on La Palma.
```

- Show how to navigate to code from HTML output

- Embed results from the `.ipynb`.

```
{{< embed notebooks/data-screening.ipynb#fig-spatial-plot >}}

@fig-spatial-plot shows the location of recent earthquakes on La Palma.
```

- Show how to navigate to code from PDF output

## Video 6: Dev container?


