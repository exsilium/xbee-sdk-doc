# About

The official XBee SDK comes with a great set of documentation that is unfortunately (to my knowledge) provided only via the SDK itself - it is embedded within the bowels of Codewarrior XBee development plugin in form of *com.digi.xbee.doc* and *com.digi.xbee.api.doc* components. This means that the documentation is accessible only via Codewarrior IDE's Help and is unreferenceable online. More pain is added by the fact that the SDK is installable only on Windows.

This library is based on the official documentation and significant effort was made to keep the formating and structure in place. The goal of this project was to make the XBee SDK documentation more accessible and readable online.

Note, however, that this documentation library is an **unofficial source** and although the SDK library does not give any warranties to the correctness of the documentation there is a possibility that through the conversion something got lost in "translation".

* If you find a mistake in this documentation, please check this against the official XBee SDK help prior to contacting Digi.

* If you find mistakes that are specific to this set of documentation, please create a github issue or submit a pull request.

## Minor Improvements

* Documentation and examples which were commented out were removed
* Only assets that are linked in documentation are included
	* XBee Extensions User's Guide asset decreased from 568 to 398
* Assets reworked for more suitable web viewing
	* XBee Extensions User's Guide weight loss of 40% (8MB in total)

## Setup

* XBee Extensions User’s Guide ([Markdown](http://daringfireball.net/projects/markdown/) / [MkDocs](http://www.mkdocs.org) / [RTD](https://readthedocs.org))
* XBee Firmware Library Documentation
	* Programming Guide ([Markdown](http://daringfireball.net/projects/markdown/) / [MkDocs](http://www.mkdocs.org) / [RTD](https://readthedocs.org))
	* API Reference ([Doxygen](http://www.doxygen.org/) / [Github Pages](https://pages.github.com))