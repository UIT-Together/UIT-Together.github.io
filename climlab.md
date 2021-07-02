# climlab

## Overview of the CLIMate LABoratory project

Brian Rose is the lead PI of the **Climate Laboratory Project**,
comprising two interconnected pieces:

- the [climlab software package](climlab_target)
- the online interactive textbook [The Climate Laboratory](book_target)

```{figure} /_static/images/ClimateLaboratory_1slide.pdf
:alt: The Climate Laboratory project, Bringing hands-on interactive climate modeling into the classroom

A one-slide public summary of the Climate Laboratory project as of October 2020
```

These initiatives were originally funded through an [NSF CAREER award](posts/2015/2015-08-19-career-grant).

(climlab_target)=
## climlab: a Python-based toolbox for process-oriented climate modeling

`climlab` is an open-ended engine for interactive, process-oriented climate modeling
for use in education and research. It is motivated by the need for simpler tools
and more reproducible workflows with which to “fill in the gaps” between
blackboard-level theory and the results of comprehensive climate models.
With `climlab` you can interactively mix and match physical model components,
or combine simpler process models together into a more comprehensive model.
`climlab` is used in the classroom (undergraduate and graduate) to put models
in the hands of students, and emphasize a hierarchical, process-oriented approach
to understanding the key emergent properties of the climate system.
`climlab` is equally a tool for climate research, where the same needs exist for
more robust, process- based understanding and reproducible computational results (Held 2005; Jeevanjee et al. 2017).

A list of `climlab`-related resources:

- The [source code on github](https://github.com/brian-rose/climlab)
- The [online documentation](http://climlab.readthedocs.io)
- The [meta-paper in Journal of Open Source Software](https://doi.org/10.21105/joss.00659)
- [Video from a presentation about `climlab`](https://ams.confex.com/ams/98Annual/videogateway.cgi/id/44948?recordingid=44948) at the AMS Python symposium (January 2018)

`climlab` is freely available under the permissive MIT license. If you find it useful
in research, teaching, or outreach, please consider reporting your usage [here on github](https://github.com/brian-rose/climlab/issues/68).

(book_target)=
## The Climate Laboratory book

***A hands-on approach to climate physics and climate modeling***

[The Climate Laboratory][book] by Brian E. J. Rose is an online, interactive textbook on fundamentals of climate science,
powered by `climlab`.

This book is powered by [JupyterBook][jupyterbook],
and aims to be all of the following:
- **self-reproducing** *(most figures are self-generating in the notebooks)*
- **free** and **open** *(permissive license, sources and content available through github)*
- **interactive** *(integration with JupyterHub and Binder will allow readers to run and modify code examples)*
- a **living document** *(content will continue to evolve, and collaboration is welcome)*

[To view the book online, go here][book].

The JupyterBook source and all book content (mostly [Jupyter Notebook][notebook] files)
are all in [this github repository][repo].

The contents of this book are licensed for free and open consumption under the
[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
license.

The book is the primary text for Brian's undergraduate Climate Laboratory (ENV 415)
and graduate Climate Modeling (ATM 623) courses at [UAlbany][ualbany]
(see [Teaching page](teaching) for links).

[ualbany]: https://www.albany.edu
[jupyterbook]: https://executablebooks.org/en/latest/tools.html#jupyter-book
[climlab]: https://github.com/brian-rose/climlab
[book]: https://brian-rose.github.io/ClimateLaboratoryBook/
[repo]: https://github.com/brian-rose/ClimateLaboratoryBook
[notebook]: https://jupyter-notebook.readthedocs.io/en/stable/
