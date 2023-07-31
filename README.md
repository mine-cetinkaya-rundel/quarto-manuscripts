# quarto-manuscripts

Slides and materials for the "Reproducible Manuscripts with Quarto" talk at posit::conf(2023).

## Video 1: Getting started with Quarto manuscripts

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

## Video 2: Multiple formats

- Show the MS Word output by downloading, then navigate in the Finder to the `_manuscript` folder
- Show the MECA bundle output in the Finder in `_manuscript` folder
- Go to `_quarto.yml` and under `formats` add
```
agu-pdf: default
```
- Re-render and show that PDF is there and styled for the journal
- Change journal to PLOS by updating `_quarto.yml`
```
pdf: default
plos-pdf:
  keep-tex: true    
```

## Video 3: Front matter

Add more to `index.qmd` YAML

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

- Re-render and show that some of these show up on the HTML and some on the PDF output (only the ones that journal requires)

