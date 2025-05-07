
# The Early Career Researcher Tool Box

This tool box aims at helping ECR going to big conferences for the first
time. It contains:

- a tutorial to make a CV webpage with a downloadable pdf version.
- a script to make a QR code directing to your webpage
- a conference bingo, what you should aim for when going to conferences

## CV as a github page

Making your CV as a github page has several advantages. It is easy to
update, it is always available, and lists of publications can be
automated. The idea is to create the CV as a quarto document, that will
be rendered both in pdf and html. Then we create a github page to host
the html version, with a button on the page to download the pdf version.
Setting up a github action, we can publish the new version of the
webpage automatically everytime a change is pushed to the main branch.

### Acknowledgement

The idea of making a webpage CV that would also be rendered in pdf was
first described in [this article from Cynthia
Huang](https://www.cynthiahqy.com/posts/cv-html-pdf/) (Huang, 2023). The
handling of lists of publications and mobile view has been added to the
original tutorial.

### Getting started

Create a quarto file named `index.qmd` (you can download the one from
the example). Fill in the information in the yaml, gather your degrees
and publications, and let’s get started!

### Short biography

The “no-print” box allows you to have a short text that appears on the
webpage version but not in the pdf. This can be modified in the css
file.

### Contact infos on mobile

For some reasons, when rendering a quarto file into an html, the table
of content and contact informations does not appear on the mobile
version. This is a massive issue, because in conferences most people
will access your page using a smartphone. The “hide-on-desktop” block
allows you to add information that will not appear on a screen larger
than 481px. This can be changed in the css file.

### Lists of publications

You can have several lists of publications: peer reviewed articles,
popular science, books, R packages, and what not. The trick is to use
the `multibib` filter, `nocite` to list publication that are not cited,
and `validate-yaml: false` to silence an unwanted error. Each list of
publication needs to be in a separated bib file. You will need to
install the multibib filter from its [github
repo](https://github.com/pandoc-ext/multibib#readme). The style of the
publication lists depend on the csl (citation style language) file.
Different csl can be downloaded on the [Zotero Style
Repository](https://www.zotero.org/styles).

### Rendering

You need to first install weasyprint, instruction can be found on [this
page](https://doc.courtbouillon.org/weasyprint/stable/first_steps.html#installation).

Then run this code to render:

``` r
quarto::quarto_render("index.qmd", output_format = "all")
```

### Making a github page

Now we want to make a github page, and we want the page to update
everytime we pull an update in the main branch. That way, you can update
your CV on another branch, and when it looks nice you open a pull
request and it updates the webpage. Side note: you can have the github
repo as private and the page as public, showing only your nicest side.

The full documentation to setup a github action can be found in the
[github
documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)

In short:

- go on your github repo, under settings \> pages
- as source, select “GitHub Actions”
- choose “static HTML”
- commit the changes to the main branch

## Making a QR code in R

QR codes are great. You can print them as stickers and have them at the
back of your phone for example. And when someone asks how to stay in
touch, or about your work, just hand it to them to scan.

BUT… most “free” QR code generators are collecting data about the people
scanning your QR code. Not cool. The `qrcode` package (Onkelinx and Teh,
2024) in R does not do that.

``` r
library(qrcode)
qrcode <- qr_code("webpage")
generate_svg(qrcode, filename = "qrcode.svg")
plot(qrcode)
```

## Conference bingo

Time to play with your colleagues!

Print this bingo, pack it and try to not yell BINGO too loud in the
middle of a session.

|                                             |                                                                  |                                                            |                                                                                |
|:-------------------------------------------:|:----------------------------------------------------------------:|:----------------------------------------------------------:|:------------------------------------------------------------------------------:|
|    Asked a question (oral presentation)     |                 Had lunch with newly met people                  | Explored the nature/culture/etc of the conference location |          Solved a science problem or puzzle I’ve been struggling with          |
|             Exchanged contacts              |                    Asked a question (poster)                     |      Went to a skills devellopment course or workshop      | Made action points for yourself about things to follow up after the conference |
|           Got a new research idea           |                Listened to a talk out of my field                |                Asked a question (any setup)                |                         Introduced myself and my topic                         |
| Went to a society or interest group meeting | Picked up a cool / useful new skill of relevance for my research |          Had a coffee or drink with a new person           |                 Shared an outstanding finding with colleagues                  |

<div id="refs" class="references csl-bib-body hanging-indent"
entry-spacing="0" line-spacing="2">

<div id="ref-huang2023" class="csl-entry">

Huang, C. (2023), “Publishing HTML and PDF versions of a Quarto CV
without LaTex”, <https://www.cynthiahqy.com/posts/cv-html-pdf/>, August.

</div>

<div id="ref-onkelinxQrcodeGenerateQrcodes2024" class="csl-entry">

Onkelinx, T. and Teh, V. (2024), *Qrcode: Generate Qrcodes with R.
Version 0.3.0*, Manual, available
at:<https://doi.org/10.5281/zenodo.5040088>.

</div>

</div>
