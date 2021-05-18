{{ template:title }}

{{ template:logo }}

{{ template:badges }}

{{ template:description }}

Welcome to Fazendaaa's {{ pkg.name }}. This is version {{ pkg.version }}!

Made with:

- [Go](https://golang.org/)
- [Docker](https://www.docker.com/)

## Ideia

Currently, in the company that I work for we have a CLI (Command Line Interface) made in [Python](https://www.python.org/) called `estat` that you can read more about it right [here](https://github.com/Fazendaaa/Succubus). But one of its features is handeling project set up, kinda like a [`create-react-app`](https://create-react-app.dev/), configuring the expcified blueprints for each language; going even further than just cloning a template git repo and than changing its values, the thing is in order to not be attached to `git`, `svn`, `mercurial` or even a new tech to come, making things the other way around by creating a project from zero to hero after asking a few questions is the safest choice.

The main ideia is that you have a `jinn.yaml` like the following describing some rules and steps to be followed when setting up a new project:

```yaml
R:
  goblal-setup:
    default-rules:
      - ask-name
      - ask-version-system
      - set-check-for-env-vars-hook
    diy-rules:
      - ask-to-publish-CRAN
      - set-lintr-file
  package:
    image: estat/r-dev # container to run the listed commands
    naming-rule: camel-case
    env-vars:
      - GITHUB_PAT=$GITHUB_PAT
    initial-packages:
      - usethis
      - testthat
      - roxygen2
    run-commands:
      - usethis::create_package($$PROJECT.NAME)
      - usethis::use_git()
      - usethis::use_github_links(auth_token = "$$GITHUB_API")
      - usethis::use_readme_md()
      - usethis::use_news_md()
      - usethis::use_roxygen_md()
      - usethis::use_testthat()
      - usethis::use_spell_check()
      - usethis::use_rstudio()
      - usethis::use_pipe()

  shiny:
    inherit-rules: package
    image: estat/shinybase
    initial-packages:
      - shiny
      - shinyjs
      - shinydashboard

Python:
  ...
Julia:
  ...
Vue:
  ...
...
```

And the a CLI prompt to ask which preset to follow -- kinda like the presets used in [Vue CLI](https://cli.vuejs.org/):

```shell
$ jinn
Which language template to start the project?
[x] R
[ ] Python
[ ] Julia
[ ] Vue
...
```

All of this is possible and without even ever needing to install R in the developer machine because of the usage of containers.

As `estat` have grown so much and making it available as FOSS (Free and open-source software) was always the idea but the project still in development and not having a properly defined scope, I decided to break its main features in other projects:

- [Succubus](https://github.com/Fazendaaa/Succubus): universal package manager based on cloud-native
- [Jinn](https://github.com/Fazendaaa/Jinn): universal project manager built to expand Succubus capabilities
- [Baba Yaga](https://github.com/Fazendaaa/BabaYaga): universal cloud-native manager built to expand Jinn and Succubus capabilities
- [Wendigo](https://github.com/Fazendaaa/Wendigo): universal project translator from cloud-native projects to other infra technologies
- [Jinn](https://github.com/Fazendaaa/Shojo): LaTex package manager
- [Hellhound](github.com/Fazendaaa/Hellhound): VSCode extension to integrate Jinn recipes
- [Crocotta](github.com/Fazendaaa/Crocotta): SOC assisted guider

## Components

### init

```shell
jinn
```

## Installing

You don't need to install Go to run this tool, just Docker. And to do so to give it a try, you can do it just by running the following line in your terminal:

```shell
alias jinn='docker run -it --volume $(pwd):/project --workdir /project fazenda/jinn'
```

And then running the following to check whether or not is working properly:

```shell
jinn --help
```

## Running

## Author

Only [me](https://github.com/Fazendaaa) because the aforementioned project was implemented by yours only. By knowing each line of that code wrote doing the port would be more easily done this way.

## Contributing

Check more about this in [CONTRIBUTING.md](CONTRIBUTING.md). Here we have a list of some of our contributors:

{{ template:contributors }}

## TODO

## References

{{ template:license }}
