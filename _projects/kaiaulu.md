---
layout: project
title: 'Kaiaulu'
caption: Mining Software Repositories in R.
description: >
  From a dissertation appendix to a collaboration tool.
date: 19-05-2023
image: 
  path: /assets/img/projects/project_kaiaulu.jpg
  srcset: 
    1920w: /assets/img/projects/project_kaiaulu.jpg
    960w:  /assets/img/projects/project_kaiaulu@0,5x.jpg
    480w:  /assets/img/projects/project_kaiaulu@0,25x.jpg
links:
  - title: Link
    url: https://github.com/sailuh/kaiaulu
accent_color: '#4fb1ba'
accent_image:
  background: '#193747'
theme_color: '#193747'
sitemap: false
---

## Kaiaulu

Kaiaulu is a [open source R package](https://github.com/sailuh/kaiaulu) for mining software repositories. This page details some 
of the design motivations behind the tool more informally. A more formal exposition was published in [ECSA 2021 LLCS](https://doi.org/10.1007/978-3-031-15116-3_6). The pre-print is [also available](https://arxiv.org/abs/2304.14570). 


### R Glue Code

Kaiaulu [began]([first commit](https://github.com/sailuh/kaiaulu/commit/224a729f44f554af311ca52cf01b105ded87499b)) as what is better described as ``R [glue code](https://en.wikipedia.org/wiki/Glue_code)''. Given a path to a project git log, Kaiaulu would then perform a 
system call passing the data to [Perceval's](https://github.com/chaoss/grimoirelab-perceval) git 
interface to transform a `.git` folder into a `.json` file. Kaiaulu would then read the `.json` into
memory and then change the `.json` to a table. At first glance, this may look like the beginning of yet another horror story: Soon, Kaiaulu would be this amalgamation of scripts no poor soul would dare be tasked to use to collect data:

<img src="https://imgs.xkcd.com/comics/data_pipeline.png" alt="XKCD Data Pipeline">
> <p><a href="https://xkcd.com/2054/">Data Pipeline</a> by <a href="https://xkcd.com/">
XKCD</a>

Instead of meeting this terrible end, I defined this very simple task in Kaiaulu as an R package. The definition of R packages follows a more structured convention, which means the code organization fits a __common abstraction__, and requires __less explanation__.

In this example, a `parse_gitlog()` function was placed in `R/parser.R`, a short Notebook `vignettes/gitlog_showcase.Rmd` explained the function and showcased the data. But isn't this obvious? Surprisingly, not so. [Pimentel et al (MSR 2019)](http://www.ic.uff.br/~leomurta/papers/pimentel2019a.pdf) found that in Python projects containing Jupyter Notebooks, only 10.3% defined local imports (i.e. imports of modules defined in the repository directory). 


### Whitebox Pipelines and Data Exploration

Research is naturally an iterative process of revisions:

<blockquote class="twitter-tweet" data-theme="dark"><p lang="en" dir="ltr">Revisions <a href="https://t.co/QnvcpVZJpz">pic.twitter.com/QnvcpVZJpz</a></p>&mdash; PHD Comics (@PHDcomics) <a href="https://twitter.com/PHDcomics/status/1299664600166789120?ref_src=twsrc%5Etfw">August 29, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

These revisions may result not only from a research advisor's feedback. It may be from a domain expert, a collaborator, a stakeholder, a publication peer-review, or even a student you are mentoring. In most cases, the interest is understanding the pipeline in plain English, not by reading code. Yet, surprisingly, MSR tools are not written in a manner to enable [literate programming](https://en.wikipedia.org/wiki/Literate_programming). The result are tables and explanations lost in e-mails or file name revisioning:

<img src="https://imgs.xkcd.com/comics/documents.png" alt="XKCD Data Pipeline">
> <p><a href="https://xkcd.com/1459/">Documents</a> by <a href="https://xkcd.com/">
XKCD</a>
 
This is unfortunate, as many assumptions, which do not carry over from project to project, are only visible in code and overlooked during revisions. Because R packages rely on an API + Notebook architecture, Kaiaulu naturally supports literate programming. Kaiaulu takes this one step further with project configuration files, distilling project-specific information used in the analysis. 

Notebooks also provide a more transparent pipeline, where anyone can understand one step of the pipeline at a time and explore the data transformations at every step of the way. Indeed, analysis discussion and collaboration now begin as a pull request in GitHub instead of e-mail threads until ready to be merged. 

### More than R Glue Code

While Kaiaulu started as means to facilitate obtaining data sources and using them on third-party tools, it has since grown to have its data representations and analysis pipelines. Refer to one of the Notebooks to get started.