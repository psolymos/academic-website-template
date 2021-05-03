# Academic website template

This template is based on the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) Jekyll theme, more specifically the adaptation of the (blog) theme to academic portfolio website by [Maximilia Kasy](https://github.com/maxkasy/home).

## Configuration

Edit the `_config.yml` file.

Navigation: edit the `_data/navigation.yml` file to change to top navigation.

Change the `assets/images/avatar.jpg` picture, make sure it is a square image otherwise the image will look like an ellipse, not a circle.

Go to your project Settings / Pages, set source to the branch you are hosting the site on (`main`, `gh-pages`), from root (`/`). Click Save, set 'Enforce HTTPS` if you like.

Use the yaml header as the following: the `author_profile` sets the profile in the sidebar.

```yaml
---
title: Welcome!
layout: academic
author_profile: true
---
```

Categories: see the `_data/categories.yml` file for the different categories that publications or software can be classified under (besides year which is kept numeric, all in press/in prep papers should get the current year and updated as published). The category `id` should match the corresponding element in the `_data/publications.yml` file, e.g. `type: "published"` etc. This is important because the IDs are used to show/hide the list elements on the page.


!!! ADD HERE HOW TO SET UP CUSTOM DOMAIN !!!

## Build

R code in the `_src` folder.

