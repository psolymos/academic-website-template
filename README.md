# Academic website template

This template is based on the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) Jekyll theme, more specifically the adaptation of the (blog) theme to academic portfolio website by [Maximilia Kasy](https://github.com/maxkasy/home).

## Configuration

### Personal info

Edit the `_config.yml` file (name, social, Googl Analytics tag, etc.).

Change the `assets/images/avatar.jpg` picture, make sure it is a square image otherwise the image will look like an ellipse, not a circle.

### Top navigation

Edit the `_data/navigation.yml` file to change to top navigation and create corresponding pages. I.e. if the link is `/nextpage/`, create a folder called `nextpage` and include an `index.md` file in it.

### Adding new pages

Use the yaml header as the following:

```yaml
---
title: Welcome!
layout: academic
author_profile: true
---
```

The `author_profile` sets the profile in the left sidebar, so keep it `true`. Change the title as needed.

### Publications

#### Categories

- see the `_data/categories.yml` file for the different categories that publications or software can be classified under (besides year which is kept numeric, all in press/in prep papers should get the current year and updated when published)
- the category `id` should match the corresponding element in the `_data/publications.yml` file, e.g. `type: "published"` etc.
- this is important because the IDs are used to show/hide the list elements on the page.

#### Publication entries

Add new publications according to this template:

```yaml
- id: Mathur2020
  text: "Mathur MB & VanderWeele TJ (2020). Sensitivity analysis for unmeasured confounding in meta-analyses. Journal of the American Statistical Association, 115(529), 163-170."
  year: 2020
  type: "methods"
  authorship: "first"
  status: "published"
  preprint:
  datarepo: "https://osf.io/2r3gm/"
  rpackagename: "EValue"
  rpackagelink: "https://CRAN.R-project.org/package=EValue"
  webappname: "EValue Calculator"
  webapplink: "https://www.evalue-calculator.com/meta/"
  doi: "10.1080/01621459.2018.1529598"
```

### GitHub pages

Go to your project Settings / Pages, set source to the branch you are hosting the site on (`main`, `gh-pages`), from root (`/`). Click Save, set 'Enforce HTTPS` if you like.

Jekyll is the default statis site builder for GitHub pages, it'll just work.

## TODO

- Range slider is using <https://refreshless.com/nouislider/>, add this to LICENSE
- Add some JavaScript so that the selector buttons and the slider show/hide the publications
- Other fields for publications? I.e. talks, media coverage.
- Classification for software
- Make the software page similar to the publications.
