A cookiecutter template for starting a dragonfly report
=======================================================

Use this template if you want to start a new report. This will produce a
skeleton directory, with a standard structure that is suitable for latex and
knitr projects in the dragonfly style.

## Making a skeleton

Firstly, install cookiecutter:

  `sudo pip install cookiecutter`
  
Then, change to the directory that will contain your report directory and run:
  
  `cookiecutter git@github.com:dragonfly-science/cookiecutter-dragonfly-report.git`
  
This will run through and ask you the following questions, either put in you
response or accept the default:

  * `author`: Put in the report authors, seperated by `and`
  * `report_slug`: The name to be used for the filename of the report, expressed as a slug (letters, characters, and dash), with no extension
  * `title`: The full report title
  * `short_title`: A short version of the title that will be used as a running header and footer
  * `subtitle`: A subtitle that is displayed on the front page, under the title
  * `bibliography`: The path and filename of the bibliography (`.bib`) file 
  * `documentclass (default is "dragonfly-report")`: The name of the latex class used for formatting the report
  * `repo_name (default is "report")`: The name of the directory that will house the report

Once this is done, you will have a directory tree that looks something like the
tree below:

```
.
└── report
    ├── discussion.Rnw
    ├── figure -> knitr/figure
    ├── introduction.Rnw
    ├── knitr
    │   └── figure
    ├── makefile
    ├── methods.Rnw
    ├── report.tex
    └── results.Rnw
```

## Using the report

Hop in to the report directory and start editing the `Rnw` files. Once you are
done, run make, and you will be away laughing.

If you want to include graphics and tables in your report, put them in `.Rnw`
files in the `knitr` directory.  This has the benefit that once they have been
made once, they will be tucked away safely, so that someone coming in to edit
the text doesn't need to get bogged down in the complexities of the knitr
files.

