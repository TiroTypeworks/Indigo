## Sources

This folder contains the source files used during the build process, as well as the design and layout sources. The build process uses output files from two different toolchains, one for design and one for layout, so any editing of the fonts may require attention to either or both.

### Source formats

**/source folder**

`.vfj` These are the canonical design sources for the Tiro Indic fonts, in FontLab 7’s JSON format. These contain all the outlines, spacing (but not kerning), and most font meta data used in the fonts.

`.input.ttf` These are the source files for the OpenType Layout tables, used by the build script. These are ‘shipped’ versions of the compiled TTFs from the /VOLT folder.

`.ufo` These are the source files for outlines etc. used by the build script. These are exported directly from the FontLab 7 `.vfj` files using the default UFO package export profile.

**/VOLT folder**

`.volt.ttf` These are TrueType font files containing the source `TSIV` tables for OpenType Layout. These can be opened and edited in Microsoft’s free Visual OpenType Layout Tool (VOLT).

`.vtp` These are corresponding plain text sources for the OpenType Layout in VOLT’s project file format. These are provided for convenience.


### Editing process

These general guidelines presume that you want to fork the project using the sources and build tools provided. There are numerous other workflows possible, and the sources can be converted to work in e.g. entirely UFO-based toolchains, or in different font editing and layout tools.

Edits to glyph set, outlines, spacing, etc. should be done in `.vfj` design sources.

Such edits then need to be incorporated into `.ufo`  files referenced in the `indigo.yml` configuration file in the /Indigo folder. Typically this will mean just replacing the `.ufo` files with new ones exported from FontLab.

Edits to OpenType Layout should be in the `.volt.ttf` sources, and then ‘shipped’ to `.input.ttf` files, replacing those in the /source folder. It is important that compiled TTFs be shipped from VOLT, not just saved, because the OTL tables that VOLT uses internally include private features and lookups that should not be included in the tables incorporated into the output fonts.

If changes are made to the glyph set, e.g. additional glyphs, in the design sources, then fresh `.volt.ttf` will need to be made. To do this, export TTFs from FontLab, then import the `.vtp` project files into these TTFs in VOLT, and edit glyph data accordingly.

The `indigo.yml` configuration file in the /Indigo folder drives the build process. It identifies the input UFO files for each font, and sets a couple of parameters:

The `names:` parameter is used to specify the version string for the font name table, which is then picked up by the build tool to set corresponding values in the name table unique ID field and the head table version field.

The `DGIG:` parameter is used to specify that a stub digital signature table should be added to the output fonts.

Other parameters are accepted by the `tirobuild.py` tool, but are not used in the Indigo project.