# Contributing to the documentation {#sec:contribute-to-docs}

## Where the documentation is

All the documentation is in the repository `duckietown/duckuments`.

The documentation is written as a series of small files in Markdown format.

It is then processed by a series of scripts to create this output:

* [a publication-quality PDF][master-pdf];
* [an online HTML version, split in multiple pages and with comments boxes][master-split].

[master-pdf]: https://book.duckietown.org/master/duckiebook.pdf
[master-html]: https://book.duckietown.org/master/duckiebook.html
[master-split]: https://book.duckietown.org/master/duckiebook/index.html
<!-- * [HTML (single-page)][master-html]; -->

## Editing links

The simplest way to contribute to the documentation is to click any of the “✎” icons next to the headers.

They link to the “edit” page in Github. There, one can make and commit the edits in only a few seconds.

## Comments

In the multiple-page version, each page also includes a comment box powered by a service called Disqus. This provides a way for people to write comments with a very low barrier. (We would periodically remove the comments.)

## Installing dependencies for compiling the documentation {#installing-docs-system}

Let `DUCKUMENTS` be the base directory for the documentation.

Download the `duckuments` repo in that directory:

    $ git clone git@github.com:duckietown/duckuments.git $DUCKUMENTS

Cd into directory:

    $ cd $DUCKUMENTS

### Setup a virtual environment

On Ubuntu 16.04, create a virtual environment usign `virtualenv` (`sudo apt install virtualenv` if needed):

    $ virtualenv --system-site-packages deploy

In other distributions you might need to use `venv`:

    $ venv deploy

Activate the virtual environment:

    $ source $DUCKUMENTS/deploy/bin/activate

Install some dependencies:

    $ sudo apt install libxml2-dev libxslt1-dev
    $ sudo apt install libffi6 libffi-dev
    $ sudo apt install python-dev python-numpy python-matplotlib

Clone the `mcdp` external repository:

    $ cd $DUCKUMENTS
    $ git clone -b duckuments git@github.com:AndreaCensi/mcdp.git

Install it and its dependencies:

    $ cd $DUCKUMENTS/mcdp
    $ python setup.py develop

(If you get a permission error here, it means you have not properly activated the virtualenv)

Depending on your system, you might need to install these other dependencies:
(It should not be necessary on Ubuntu 16 given the `apt` commands above.)

    $ cd $DUCKUMENTS
    $ pip install numpy matplotlib

Ensure the latest version (>6) of `nodejs` is installed.

Run:

    $ nodejs --version
    6.xx

If the version is 4 or less, remove `nodejs`:

    $ sudo apt remove nodejs

Install `nodejs` using [the instructions at this page][nodejs].

[nodejs]: https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions

<!-- $ sudo apt install node-less -->

Next, install the necessary Javascript libraries using `npm`:

    $ cd $DUCKUMENTS
    $ npm install MathJax-node jsdom@9.3 less

Install PrinceXML from [this page](https://www.princexml.com/download/).

Download STIX fonts from [this site][stix].

[stix]: https://sourceforge.net/projects/stixfonts/files/latest/download

Unzip and copy the ttf to `~/.fonts`:

    $ cp -R STIXv2.0.0 ~/.fonts

and then rebuild the font cache using:

    $ fc-cache -fv


## Troubleshooting installation problems

### Installing `nodejs` packages

The only pain point  in the installation procedure has been the installation of `nodejs` packages using `npm`. For some reason, they cannot be installated globally (`npm install -g`).

Do not use `sudo` for installation. It will cause problems.

If you use `sudo`, you probably have to delete a bunch of directories,
such as: `RBROOT/node_modules`, `~/.npm`, and `~/.node_modules`, if they exist.


## Compiling the documentation

Make sure you have deployed and activated the virtual environment. Then:

    $ cd $DUCKUMENTS
    $ make duckuments-dist

This creates the directory `duckuments-dist`, which contains
another checked out copy of the repository, but with the branch `gh-pages`, which
is the branch that is published by Github using the "Github Pages" mechanism.

At this point, please make sure that you have these two `.git` folders:

    $DUCKUMENTS/.git
    $DUCKUMENTS/duckuments-dist/.git

To compile the docs, go in the `DUCKUMENTS` directory and run `make compile`:

    $ cd $DUCKUMENTS
    $ make clean compile

If you want to do incremental compilation, you can omit the `clean` and just
use:

    $ make compile

To compile the PDF, use:

    $ make compile-pdf

This creates the following files:

* `duckuments-dist/master/duckiebook.html` is a single-page HTML of everything.
* `duckuments-dist/master/duckiebook.pdf` is the PDF version.
* `duckuments-dist/master/duckiebook/index.html` is the first page of the version with each chapter on a different page.

## Deploying the documentation

**This is now done by a bot.**

To deploy the documentation, jump into the `DUCKUMENTS/duckuments-dist` directory.

Run the command `git branch`. If the out does not say that you are on the branch `gh-pages`,
then one of the steps before was done incorrectly.

    $ cd $DUCKUMENTS/duckuments-dist
    $ git branch
    ...
    * gh-pages
    ...

Now, after triple checking that you are in the `gh-pages` branch, you can
use `git status` to see the files that were added or modified,
and simply use `git add`, `git commit` and `git push` to push the files
to Github.
