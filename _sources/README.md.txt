# Rose Research Group Website

![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/brian-rose/brian-rose.github.io/deploy-site/main?logo=github&style=for-the-badge)

Sphinx source for the website currently deployed simultaneously in two different places:
-  <http://www.atmos.albany.edu/facstaff/brose/>
- <https://brian-rose.github.io>

## How it works

The static site is built automatically using GitHub Actions and deployed to https://brian-rose.github.io.
To see how this works, look at `.github/workflows/deploy.yaml` in the source repository.
To mimic this workflow in another repository, note that you need to enable GitHub Pages
for your repo (Setting --> Options --> GitHub Pages).


## How to make changes to the site

Rose group members and collaborators are welcome to open Pull Requests with proposed changes. PRs are automatically rendered on readthedocs.org for viewing changes. Select the `Show all checks` link in the PR discussion to reveal the link to `readthedocs.org`. If something doesn't look right, make changes and push to the same branch from where you opened the PR and they will be re-rendered.

Note that the [people page](https://brian-rose.github.io/people.html) is generated at build time from data in the file [_data/people.yml](https://github.com/brian-rose/brian-rose.github.io/blob/main/_data/people.yml). Add yourself and edit your details through this file. Add your headshot image to [_static/images](https://github.com/brian-rose/brian-rose.github.io/tree/main/_static/images). I also encourage everyone to add their preferred pronouns.


## How to build the site locally

You can also built the static site manually by installing sphinx and all dependencies in a python environment. For example, from the source repository:
```
pip install -r requirements.txt
make html
```

You can now view the built site in your web browser with
```
open _build/html/index.html
```
