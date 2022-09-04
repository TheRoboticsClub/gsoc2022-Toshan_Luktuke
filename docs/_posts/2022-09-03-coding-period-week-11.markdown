---
layout: posts
title:  "Week 11: Coding Period"
date:   2022-09-04 15:52:32 +0530
categories: gsoc
---

Going by the suggestions of my mentors, I spent this week working on the documentation of the blocks and some updates to my blog.

## Documentation

After a meet with my mentors, I spent some time organising the documentations files. Then I changed the theme to dark mode to go with the overall look of Visual Circuit Website. Once that was done I made a Pull Request integrating the changes to the `docs` branch of the repo.

Next we'll merge it with the main website. However, I have to make some decisions about how to update the docstrings in the actual JSON files. Namely there's still the issue of updating all of the docstrings in the template files themselves.

Additionaly if we are to add some extra info the docs by ourselves, it'll be lost when the updating script is run. In this case it makes sense to have a separate repo somewhere with all the documentation data.

## Blog updates

I updated this blog a bit as well, adding some images, descriptions and generally just improving its look a bit in this week.


## Issues
No new issues were raised this week

## Pull Requests
- [Add new documentation for Blocks made by pdoc](https://github.com/JdeRobot/VisualCircuit/pull/187) (This is by far the largest pull request simple because of the amount of lines added XD)
