Starting a new dragonfly report
=======================================================

Use this template to start a new report. This will produce a
skeleton directory, with a standard structure that is suitable for `latex` and
`knitr` projects in the dragonfly style.

## Making a skeleton

Firstly, install cookiecutter:


  `sudo easy_install pip` (use this line if you don't already have `pip`)
  
  `sudo pip install cookiecutter`
  
Then, change to the directory that will contain your report directory and run:
  
  `cookiecutter git@github.com:dragonfly-science/cookiecutter-dragonfly-report.git`
  
This will run through and ask you the following questions, either put in you
response or accept the default:

  * `author`: Put in the report authors, separate multiple authors by `\and`
  * `report_slug`: The name to be used for the filename of the report, expressed as a slug (letters, characters, and dash), with no extension
  * `title`: The full report title
  * `short_title`: A short version of the title that will be used as a running header and footer
  * `subtitle`: A subtitle that is displayed on the front page, under the title
  * `bibliography`: The path and filename of the bibliography (`.bib`) file 
  * `documentclass (default is "dragonfly-report")`: The name of the latex class used for formatting the report
  * `repo_name (default is "report")`: The name of the directory that will house the report
  * `file_extension (default is "rnw")`: Is the file extension that will be used for `Rnw` files. This
is to allow for differences in case and also for `Rtex` files. 
  * `build_directory (default is "build")`: a directory to hold all the intermediate files

Once this is done, you will have a directory tree that looks something like the
tree below:

```
.
└── report
    ├── .gitignore
    ├── discussion.Rnw
    ├── introduction.Rnw
    ├── knitr
    │   └── figure
    ├── makefile
    ├── methods.Rnw
    ├── report.tex
    └── results.Rnw
```

## Writing a report

Hop in to the report directory and start editing the `Rnw` files. Once you are
done, run make, and you will be away laughing.

If you want to include graphics and tables in your report, put them in `.Rnw`
files in the `knitr` directory.  This has the benefit that once they have been
made once, they will be tucked away safely, so that someone coming in to edit
the text doesn't need to get bogged down in the complexities of the `knitr`
files. These files can be included in the document without their paths. 

