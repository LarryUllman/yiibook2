# "The Yii Book" (2nd edition) by Larry Ullman

This is the source material for "The Yii Book" (2nd edition), written by Larry Ullman and published 2015-2024. 

The book was written in [Scrivener](https://www.literatureandlatte.com/scrivener/overview) and then exported in MulitMarkdown (.mmd) format. 

Proper and ~decent PDF layout requires [LaTeX](https://www.latex-project.org). For the chapters to be created properly in LaTeX, this command was then run:

```bash
sed -i '.bak' -E 's/(FUNDAMENTAL CONCEPTS|STARTING A NEW APPLICATION|A MANUAL FOR YOUR YII SITE|INITIAL CUSTOMIZATIONS AND CODE GENERATIONS|WORKING WITH MODELS|WORKING WITH VIEWS|WORKING WITH CONTROLLERS|WORKING WITH DATABASES|WORKING WITH FORMS|MAINTAINING STATE|USER AUTHENTICATION AND AUTHORIZATION|WORKING WITH WIDGETS|USING EXTENSIONS|JAVASCRIPT AND JQUERY|INTERNATIONALIZATION|LEAVING THE BROWSER|IMPROVING PERFORMANCE|ADVANCED DATABASE ISSUES|EXTENDING YII|WORKING WITH THIRD-PARTY LIBRARIES|TESTING YOUR APPLICATIONS|CREATING A CMS|MAKING AN E-COMMERCE SITE|SHIPPING YOUR PROJECT) /# \1 #\
\
/g' yiibook2.mmd
```

That's a global replace, using `sed`. 

[Pandoc](https://pandoc.org) was used to create PDF versions of the book:

```bash
pandoc yiibook2.mmd -o yiibook2.pdf --toc --top-level-division=chapter --template=src/default.template --highlight-style=tango --pdf-engine=xelatex
```

Pandoc required **default.template** for layout, frontmatter, and so forth.

Pandoc was also used to create ePub versions of the book:

```bash
pandoc -o yiibook2.epub -t epub3 yiibook2.mmd src/metadata.yaml
```

For the ePub, metadata is pulled from a YAML file.

[Calibre](https://calibre-ebook.com) was used to create MOBI versions of the book:

```bash
/Applications/calibre.app/Contents/MacOS/ebook-convert yiibook2.epub yiibook2.mobi
```

It uses the ePub as the source, so that must be created first. This command assumed Calibre was installed on a Mac.
