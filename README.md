# RESTful-PDF-Metadata-Updater
A simple command line PDF metadata editor that pulls info from the Google Books Dynamic Links API.

## Description

The Restful PDF Metadata Updater takes advantage of the [_Google Books Dynamic Links_](https://developers.google.com/books/docs/dynamic-links) API, which in their own words, "allows you to create more customizable, reliable links to Google Books."

The script works by taking the PDF filename and user inputs and building an API call around it. It then parses the returned _JSON_ data and prompts the user for correctness. After this it overwrites the PDF's author, title, and moddate fields while retaining everything else.

## Usage
```
useage: change-metadata.py -p PATH [-o OUTPUT] [-a AUTHOR NAME] [-b BOOKMARK PARSER] [-v VERBOSE]

arguments:
-p PATH,   --path PATH                  Your PDF's filepath
-o OUTPUT, --output OUTPUT              Desired output location of the updated PDF,
                                          writes to initial path if omitted
-a AUTHOR NAME, --author                Optional argument to include the author's
                                          name for better search results.
-b BOOKMARK PARSER, --debug_bookmark    Used for instances of erroneous values encoded
                                          in the new documents outline.
-v VERBOSE, --verbose                   When called suppresses the metadata
                                           confirmation prompt.
```

The `path` field is the only one required to run, everything else is optional. However, the `author` field is recommended, as the API supports search by author. 
The `-b` argument is an optional flag to call the `outline_rebuilder` method. This is to deal with string-encoding issues that can arise when `pypdf` reads PDFs with nested outlines (bookmarks).

## Example
The following command will get the metadata for _Statistical Inference_ by George Casella.
```sh
python change-metadata.py -p "Statistical Inference.pdf" -o "C:\Users\user\Statistical Inference.pdf" -a "George Casella"
```
If you want to edit a number of files at once, copy the file paths to a _.txt_ file and pass it like any other PDF.
```sh
python change-metadata.py -p "files_to_update.txt"
```
