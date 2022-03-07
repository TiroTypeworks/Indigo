![Indigo](https://github.com/TiroTypeworks/Indigo/blob/main/docs/images/indigobanner_2000.png)
## About Indigo

**5 March 2022**

Indigo is a project in four parts: a tranche of fonts for some of the major Indian writing systems; design and layout sources for these fonts; detailed written documentation regarding the design and production of these fonts; and a suite of test documents.

*The first two parts of the Indigo project are made public in early March 2022; the remaining two parts are in-progress (hence, some parts of the repo structure are empty except for license texts for the intended content).*

The eight font families in the Indigo project are

* Tiro Bangla
* Tiro Devanagari Hindi
* Tiro Devanagari Marathi
* Tiro Devanagari Sanskrit
* Tiro Gurmukhi
* Tiro Kannada
* Tiro Tamil
* Tiro Telugu

## Font build process

**[For detailed instructions on editing and working with the various source files, please see the [readme file in the /source folder](https://github.com/TiroTypeworks/Indigo/blob/master/source/README.md).]**

This repo contains the source files and build tools needed to output a set of the Indigo project fonts. The build process is scripted, and uses a simple YAML configuration file, and `tirobuild.py` tool, and a number of required open source libraries. For details of the source files, including the YAML configuration file in this folder, please see the readme file in the /source folder.

Latest official builds of the fonts are always available in the /fonts folder. The following build process only needs to be used if you are editing any of the sources, e.g. if you intend to fork the project and want to continue to use the Tiro build process. Note that the `indigo.yml` configuration file will rebuild the entire collection of Tiro Indic fonts. If you wish to only build select fonts, create a custom YAML configuration file for each font or set of fonts.

After cloning this repo locally:

1) Create a virtual environment at the Indigo folder level:

```
$ cd [path]/Indigo 
$ python3 -m venv venv
```

2) Activate virtual environment:

```
$ source venv/bin/activate
```

3) Install dependencies:

```
pip3 install -r requirements.txt
```

4) Run the build script (it will take several minutes to complete the build process):

```
$  python tools/tirobuild.py indigo.yml
```

**All four steps are only necessary for the initial build: for subsequent builds only steps (2) and (4) should be necessary.**

The build process will generate the new font files in an /output folder. Output formats include CFF and TTF flavours of OpenType, and WOFF2 and WOFF webfonts of each. The sequence of build operations is:

* build TTF/OTF from UFO files
* remove overlaps
* copy OTL tables from input.ttf sources
* autohint (ttfautohint and AFDKO)
* optimise
* build WOFF2/WOFF

*Note that the /fonts folder in the repo contains pre-built compiled fonts provided for convenience by Tiro Typeworks. The build process does not overwrite these fonts, so remember to look in the /output folder that the build process creates for locally built fonts.*
