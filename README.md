# PDFreactor files for testing

This repo contains a number of examples, illustrating how PDFreactor can be used in 
Booktype. To be more precise: information on what a new export script needs to be
capable of, to create the HTML and CSS which is needed by PDFreactor.

Booktype is currently creating PDF files with mpdf. Orphans, widows and hyphenation
are not managed well by mpdf, which is why we add the option to create PDFs using
the proprietary PDFreactor solution. 

(Other proprietary export renderers can be added, like PrinceXML. We decided to
go with PDFreactor, because their support of baseline-grid is making it that bit
more attractive. The open source version of vivliostyle is impressive, but does not 
support hyphenation... yet. For details, see the great site http://www.print-css.rocks/ ).

If you have PrinceXML installed, you can also create PDFs from the HTML/CSS files
to get an impression of what they will come out like. In your terminal, move to the
folder with the HTML/CSS file and type (e.g.):

`prince -s pdfreactor-style.css pdfreactor-body.html -o princexml.pdf`

## Structure

* `samples/` contains the folders with relevant HTML, CSS files
* `samples/Fonts/` contains all fonts used anywhere in the CSS samples
* `lib/` contains the PDF wrapper for PDreactor 

### Inside a sample directory

There are sample PDF files:
* `samples/BT_theme_academic/static_mpdf_test.pdf`
* `samples/BT_theme_academic/static_pdfreactor_test.pdf`

There are the mpdf HTML and CSS files for reference:
* `samples/BT_theme_academic/mpdf-endmatter.html`
* `samples/BT_theme_academic/mpdf-frontmatter.html`
* `samples/BT_theme_academic/mpdf-body.html` (this is the mainmatter)

And there are the PDFreactor files which will be rendered. If you start a new sample folder, make sure
they are named like the following, because this is what the php file is looking for:
* `samples/BT_theme_academic/pdfreactor-body.html`
* `samples/BT_theme_academic/pdfreactor-style.css`

The following two CSS files are included by `pdfreactor-style.css`. 
They are optional - including the fonts and page size:
* `samples/BT_theme_academic/_PDFRfonts.css`
* `samples/BT_theme_academic/_PDFRpagesize.css`

## Install and run the PDFreactor web service

The PDFreactor web service is required to be running even when using PDFreactor on the command line.

* Download the PDFreactor archive from http://www.pdfreactor.com/download/ and extract it on the local system. The directory `PDFreactor` should be created.
* Change to the `PDFreactor/bin/` directory
* Run `./pdfreactorwebservice start`
* Check if the web service is running with `./pdfreactorwebservice status`
* The web service will start accepting requests a few seconds later. Until then, you may see: `<urlopen error [Errno 111] Connection refused>` when attempting to use it.

## Running PDFreactor from the command line

The syntax to create PDF files using the command line is:

`./pdfreactor.py -i input.html -o output.pdf`

Important: the CSS file needs to be in the same directory and the CSS file needs to be linked in the
header of the HTML file. Inside the CSS file, you need to link to the font files as a relative path.

## PHP wrapper script

* Open the file `index.php` from this repository and change the relative paths to match the HTML and CSS file you want to use for PDF rendering.
* Make sure this repo is available through your browser on localhost, e.g. with Apache.
* Open the URL in a browser (e.g. `http://localhost/pdfreactor-examples/`).
