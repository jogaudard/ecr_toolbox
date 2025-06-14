
# A Tool Box for Early Career Researchers going to big conferences

This tool box aims at helping ECR going to big conferences for the first
time. It contains:

- a tutorial to make a CV webpage with a downloadable pdf version.
- a script to make a QR code directing to your webpage
- a conference bingo, what you should aim for when going to conferences

Feel free to suggest content (via a github issue ideally) or fork it and
adapt it as you please.

## CV as a github page

Making your CV as a github page has several advantages:

- It is easy to update and maintain. My trick is to put everything in
  the working file, and pass as comments what I currently do not want to
  show.
- It is always available, as long as there is internet, which is great
  for networking.
- Lists of publicatons are easier to handle
- It looks cool (I might be biased on that one).

The idea is to create the CV as a quarto document, that will be rendered
both in pdf and html. Then we create a github page to host the html
version, with a button on the page to download the pdf version. Setting
up a github action, we can publish the new version of the webpage
automatically everytime a change is pushed to the main branch. See the
example [here](https://jogaudard.github.io/ecr_toolbox/).

### Acknowledgement

The idea of making a webpage CV that would also be rendered in pdf was
first described in [this article from Cynthia
Huang](https://www.cynthiahqy.com/posts/cv-html-pdf/) (Huang, 2023). The
handling of lists of publications, mobile view, and github page
automation have been added to the original tutorial.

### Getting started

Generate a new repository from this template, gather your degrees and
publications, and let’s get started! For a basic use, you will only need
to edit the `index.qmd` (that is the CV itself), the files in the
`publications` folder, and the QR code code chunk. If you wish to modify
the layout, you will need to modify `cv.css` as well. In the
`index.qmd`, you need to fill in your own information in the yaml and
the short biography, and add the sections you need. Bibliographies will
be done using bibtex (see below).

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
popular science, books, R packages, and what not. Each list of
publication needs to be in a separated bib file, that you call in the
yaml. You change the citation style by changing the citation style
language file (csl). Different csl can be downloaded on the [Zotero
Style Repository](https://www.zotero.org/styles). Change the
`bold-auth-name:` in the yaml to have your name appear in bold. And for
publication with many authors where your name does not appear, the trick
is to manually change the entry in the bib file to get your name higher
in the list.

All of this works with the
[multibib](https://github.com/pandoc-ext/multibib#readme) and
[bold-author](https://stackoverflow.com/a/76429867/10685715) extensions,
in case you want to dive deeper.

Editing the `emaillart_publications.qmd` file, you can make a list of
publications in pdf (that gets updated everytime you render it) that can
be downloaded from the CV webpage.

### Rendering

You need to first install weasyprint, instruction can be found on [this
page](https://doc.courtbouillon.org/weasyprint/stable/first_steps.html#installation).

Then run this code to render:

``` r
quarto::quarto_render("index.qmd", output_format = "all")
quarto::quarto_render("emaillart_publications.qmd")
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

Your CV is now online with an address that looks like this:
[username.github.io/\[cv_repo_name\]](https://jogaudard.github.io/ecr_toolbox/)!

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

|                                             |                                                                  |                                                            |                                                               |                                                                                |
|:-------------------------------------------:|:----------------------------------------------------------------:|:----------------------------------------------------------:|:-------------------------------------------------------------:|:------------------------------------------------------------------------------:|
|    Asked a question (oral presentation)     |                 Had lunch with newly met people                  | Explored the nature/culture/etc of the conference location | Solved a science problem or puzzle I’ve been struggling with  |                                 Helped someone                                 |
|        Exchanged contact information        |                    Asked a question (poster)                     |      Went to a skills devellopment course or workshop      | Attended a presentation or workshop around inclusivity topics | Made action points for yourself about things to follow up after the conference |
|  Met with a former colleague / supervisor   |                Listened to a talk out of my field                |                Asked a question (any setup)                |                Introduced myself and my topic                 |                            Got a new research idea                             |
| Went to a society or interest group meeting | Picked up a cool / useful new skill of relevance for my research |          Had a coffee or drink with a new person           |         Shared an outstanding finding with colleagues         |            Attended a presentation or workshop about mental health             |

<!-- --------------------------------------------- ------------------------------------------------------------------- ------------------------------------------------------------- -------------------------------------------------------------------------------- 
      Asked a question (oral presentation)                       Had lunch with newly met people                    Explored the  nature/culture/etc of the conference location            Solved a science problem or puzzle I've been struggling with           
               Exchanged contacts                                   Asked a question (poster)                             Went to a skills devellopment course or workshop        Made action points for yourself about things to follow up after the conference  
            Got a new research idea                             Listened to a talk out of my field                                  Asked a question (any setup)                                          Introduced myself and my topic                          
  Went to a society or interest group meeting   Picked up a cool / useful new skill of relevance for my research              Had a coffee or drink with a new person                              Shared an outstanding finding with colleagues                  
 --------------------------------------------- ------------------------------------------------------------------- ------------------------------------------------------------- --------------------------------------------------------------------------------  -->

## Conference DOs

- Have a couple of A4 prints of your poster with you at all times.
- Have your slides on your phone (true story: I redid my presentation to
  some important people who had missed it on the U1 in Vienna at 23:00
  from my phone slides.)
- Reach out to your network (former supervisor, people met on a course,
  …) before the conference and get organised to meet.
- Use your university email. Most big conferences have a tool to find
  people with their email.
- Take it easy, escape once in a while, do sports (or whatever provides
  you balance).

<!-- ## Conference DON'Ts -->

### References

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
