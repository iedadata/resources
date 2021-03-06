# Sitemap tools for IEDA

This directory contains files for generating a sitemap.xml file for metadata in the web-accessible get.iedatada.org/doi.

## Files:

### index.php
PHP page that produces a sitemap index from the content of a directory located at ../metadata/iso (relative to the location where the page is deployed). A separate sitemap file is produced in the same directory as the PHP page named {dirname}_sitemap.xml for each subdirectory at ../metadata/iso.  The index file produced by this page is xml, and has a header stylesheet directive pointing at xml-sitemap.xsl in the same directory that yields an html view in a browser.  The Sitemap index is accessed at http://get.iedata.org/sitemaps

### DOIxml-sitemap.php
This PHP page displays a sitemap from the IEDA get.iedatada.org/doi directory, which contains datacite XML metadata  for the EarthChem Library (ECL) and Marine-Geo Digital Library (MGDL).  GETS from the http://get.iedadata.org/doi/ directory are redirected by the .htaccess file to transform the xml to html; the transformation inserts a schema.org JSON-LD script in the html <head> section for use by google and other search engines.  The code for the transformations is located in https://github.com/iedadata/resources/tree/master/DataCiteXMLTransforms

Read more about the original code here: [XML Sitemap PHP script](http://yoast.com/xml-sitemap-php-script/).

### config.php
sets locations to read files that will be added to the sitemap, the location of the sitemap xml to html XML transform file (currently in same directory), and a couple of options for program execution; see comments in file.

### xml-sitemap.xsl
xml transform that converts sitemap or sitemap index xml into html files for viewing in a browser.  Invoked by an <?xml-stylesheet... directive in the headers for the sitemap.xml file.  Works for a sitemap or sitemap index file.

### jdevalk-XML-Sitemap-PHP-Script
link to original location where the php script was found. location is https://github.com/jdevalk/XML-Sitemap-PHP-Script

### config-sample.php
Config file with dummy values to use as starter for creating custom config files in new environments

## Configuration

Open the config.php file and configure the settings for the sitemap generation. 
Then check the output and if it's ok, add the script URL to Google Webmaster Tools.

## Deployment

### Original DataCite based workflow:

xml-sitemap.php, config.php and xml-sitemap.xsl are copied to seafloor /public/mgg/web/get.iedadata.org/htdocs/doi. 
XML sitemap based on the DataCite records can then be accessed at http://get.iedadata.org/doi/xml-sitemap.php. This is the original workflow implemented.

### Workflow for ISO records:

at seafloor /public/mgg/web/get.iedadata.org/htdocs/,  place the index.php and xml-sitemap.xsl files in direcory named 'sitemaps'.  

The metadata/iso directory in htdocs should be configured according to the instructions in the GitHub IEDA/resources/iedaisoschemaorg repository readme.md. Each IEDA partner system should have a separate subdirectory in /metadata/iso, containing ISO xml files. Currently the ISO files have different naming conventions that the index.php script handles; the default we should use in the future is NNNNNN_iso.xml to make thing simpler.  The 6 digit DOI token numbers are used to construct requests like get.iedadata.org/metadata/NNNNNN that GET an HTML view of the ISO record with the Schema.org JSON-LD script in the header.


## Changelog

* 2018-01-23:
    * SMR download from Yoast website and configure for use with IEDA Datacite DOI directory xml. 
	
	Write urls to access the html view of the datacite record generated by dataciteToHTMLwithSDO.xsl that includes schema.org markup. 
    
* 2018-05-10: 
    * SMR rename original DOI DataCite xml sitemap producer php to DOIxml-sitemap.php, and add new index.php that generates a sitemap index, and is designed to deploy in a sitemap directory. Update this readme
