epubQTools [![Release](https://img.shields.io/github/release/johnykvsky/epubqtools.svg)](https://github.com/johnykvsky/epubqtools/releases/latest)
==========

Tools for checking, correcting and hyphenating EPUB files. Created by [quiris11][link-author] under GNU Affero General Public License. 

This version was updated to work with Python v3.

#### Changes in this version

 - disclaimer: this version was tested only on linux, with latest epubcheck (4.2.4) and kindlegen (v2.9 build 1028-0897292 for Linux)
 - it was updated to work with Python v3, at the moment it's 3.7
 - it was slightly modified to work with unpacked epubcheck instead of extracting it on every run to /tmp directory
 - it also shows epubcheck version (if it's used)

#### External apps used by this tool available for download:

* **kindlegen**: https://github.com/koenrh/docker-kindlegen/tree/master/kindlegen
* **epubcheck-4.2.4.zip** (Java installed is required to run it): https://github.com/IDPF/epubcheck/releases

#### Additional requirements:
* python -m pip install lxml
* python -m pip install cssutils

#### Mini how-to

 Download both external tools and put them in **tools** folder. Tools folder should contain:

 - `kindlegen` file, marked as executable (from kindlegen_linux_2.6_i386_v2_9.tar.gz archive)
 - `epubcheck.jar` file, marked as executable (from epubcheck-4.2.4.zip archive)
 - `lib` directory with `*.jar` files (also from epubcheck-4.2.4.zip archive)

 Create runnable zip file with epubQTools. Just zip all files in this repository. So it should contain (as is, not in any additional subfolder):
 - `__main__.py`
 - `lib` with all it's content

 Then you can run. I run following script:

 ```
python3.7 epubQTools.zip ./epub -V
python3.7 epubQTools.zip ./epub -n -l ./log --tools ./tools
python3.7 epubQTools.zip ./epub -q -l ./log --tools ./tools
python3.7 epubQTools.zip ./epub -e -l ./log --tools ./tools
python3.7 epubQTools.zip ./epub -qm -l ./log --tools ./tools
python3.7 epubQTools.zip ./epub -pm -l ./log --tools ./tools
python3.7 epubQTools.zip ./epub -kd -l ./log --tools ./tools
 ```

Where `epub` folder contains `.epub` files I want to process, `log` folder store logs from file processing and `tools` folder contains tools (as mentioned before).

But you don't have to create zip file, epubQTools ean be run like this (just point to `__main__.py` file): `python3.7 epubQTools/__main__.py -V`

#### Documentation

```
usage: epubQTools [-h] [-V] [--tools [DIR]] [-l [DIR]] [-i [NR]]
                  [--author [Surname, First Name]] [--title [Title]]
                  [--font-dir [DIR]] [--replace-font-family [old,new]] [-a]
                  [-n] [-q] [-p] [--list-fonts] [-m] [-e] [--skip-hyphenate]
                  [--skip-hyphenate-headers] [--skip-reset-css]
                  [--skip-justify] [--left] [--replace-font-files] [--myk-fix]
                  [--remove-colors] [--remove-fonts] [-k] [-d] [-f]
                  [--fix-missing-container] [--book-margin [NUMBER]]
                  directory

positional arguments:
  directory             Directory with EPUB files stored

optional arguments:
  -h, --help            show this help message and exit
  -V, --version         show program's version number and exit
  --tools [DIR]         path to additional tools: kindlegen, epubcheck
  -l [DIR], --log [DIR]
                        path to directory to write log file. If DIR is omitted
                        write log to directory with epub files
  -i [NR], --individual [NR]
                        individual file mode
  --author [Surname, First Name]
                        set new author name (only with -i)
  --title [Title]       set new book title (only with -i
  --font-dir [DIR]      path to directory with user fonts stored
  --replace-font-family [old,new]
                        pair of "old_font_family,new_font_family"(only with -e
                        and with --font-dir)
  -a, --alter           alternative output display
  -n, --rename          rename .epub files to 'author - title.epub'
  -q, --qcheck          validate files with qcheck internal tool
  -p, --epubcheck       validate epub files with EpubCheck 4 tool
  --list-fonts          list all fonts in EPUB (only with -q)
  -m, --mod             validate only _moh.epub files (works only with -q or
                        -p)
  -e, --epub            fix and hyphenate original epub files to _moh.epub
                        files
  --skip-hyphenate      do not hyphenate book (only with -e)
  --skip-hyphenate-headers
                        do not hyphenate headers like h1, h2, h3...(only with
                        -e)
  --skip-reset-css      skip linking a reset CSS file to every xthml file
                        (only with -e)
  --skip-justify        skip replacing "text-align: left" with "text-align:
                        justify" in all CSS files (only with -e)
  --left                replace "text-align: justify" with "text-align: left"
                        in all CSS files (experimental) (only with -e)
  --replace-font-files  replace font files (only with -e)
  --myk-fix             fix for MYK conversion oddity (experimental) (only
                        with -e)
  --remove-colors       remove all color definitions from CSS files (only with
                        -e)
  --remove-fonts        remove all embedded font files (only with -e)
  -k, --kindlegen       convert _moh.epub files to .mobi with kindlegen
  -d, --huffdic         tell kindlegen to use huffdic compression (slow
                        conversion) (only with -k)
  -f, --force           overwrite previously generated _moh.epub or .mobi
                        files (only with -k or -e)
  --fix-missing-container
                        Fix missing META-INF/container.xml file in original
                        EPUB file (only with -e)
  --book-margin [NUMBER]
                        Add left and right book margin to reset CSS file (only
                        with -e)
```

#### Tip

To read/check ebooks on linux use [foliate][link-foliate]

[link-author]: https://github.com/quiris11/epubQTools
[link-foliate]: https://johnfactotum.github.io/foliate/