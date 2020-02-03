# Notes on initial variable font builds
Stephen Nixon (@ArrowType), 2020-01-31

*(start 12:30)*

1. Make `venv`
2. Add `requirements.txt`
3. Make basic `build.sh` shell script for fontmake + file sorting

### Tilt Neon

Trying to build `sources/Tilt Neon/Rotated/Tilt-Neon.designspace`.

First obstacle:

```
cu2qu.errors.IncompatibleFontsError: fonts contains incompatible glyphs: 'Aogonek', 'Ccedilla', 'caron', 'caroncmb', 'cedilla', 'cedillacmb', 'circumflex'
```

*(Pause 12:40)*
*(Start 17:40)*

Because this is a cu2qu conversion error, I'll check that all segments are strictly compatible.

To do so, I'll adapting a shell script to check segments in masters: `sources/mastering-scripts/check-segments-selected-masters.py`

![Segment check for Aogonek in Tilt Neon masters, showing incompatibilities](assets/2020-01-31-17-52-21.png)\

Full results:

```
type-repos/google-font-repos/Tilt-Typeface  mastering ✗                                                                                                                                                                                                                                          26m ◒  
▶ python sources/mastering-scripts/check-segments-selected-masters.py "sources/Tilt Neon/Rotated" "Aogonek Ccedilla caron caroncmb cedilla cedillacmb circumflex"
Getting UFO paths
['Aogonek', 'Ccedilla', 'caron', 'caroncmb', 'cedilla', 'cedillacmb', 'circumflex']
['SubSource-HROTx_VROTdd.ufo', 'Source-HROTd_VROTd.ufo', 'SubSource-HROTn_VROTdd.ufo', 'SubSource-HROTdd_VROTd.ufo', 'SubSource-HROTd_VROTdd.ufo', 'Source-HROTx_VROTn.ufo', 'Source-HROTx_VROTx.ufo', 'Source-HROTn_VROTd.ufo', 'Source-HROTn_VROTn.ufo', 'SubSource-HROTdd_VROTdd.ufo', 'Source-HROTn_VROTx.ufo', 'Source-HROTx_VROTd.ufo', 'Source-HROTd_VROTx.ufo', 'Source-HROTd_VROTn.ufo', 'SubSource-HROTdd_VROTn.ufo', 'SubSource-HROTdd_VROTx.ufo']


Segment types: 🥐 = curve | 📏 = line | 🚚 = move | 🥨 = qcurve

FONT                            | /Aogonek: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 22] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /Ccedilla: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 12] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 12] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 10] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 12] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 12] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 12] 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C01 [segs 10] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /caron: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /caroncmb: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /cedilla: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 10] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /cedillacmb: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 10] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /circumflex: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
```

### Tilt Prism

Trying to build `sources/Tilt Prism/Rotated 03 Combined/Tilt-Prism.designspace`.

```
cu2qu.errors.IncompatibleFontsError: fonts contains incompatible glyphs: 's'
```

Segments:

```

FONT                            | /s: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTd_VROTn.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 📏 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTd_VROTx.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTn_VROTd.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTn_VROTn.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 📏 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTn_VROTx.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTx_VROTd.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTx_VROTn.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 📏 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
Source-HROTx_VROTx.ufo          | C00 [segs 24] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏  | C01 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C02 [segs 08] 📏 🥐 📏 📏 📏 🥐 📏 📏  | C03 [segs 19] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐 🥐  | C04 [segs 19] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 📏 📏 🥐 🥐 🥐 🥐 🥐 🥐 📏  | 
```

### Tilt Warp

Trying to build with `sources/Tilt Warp/Rotated/Tilt-Warp.designspace`. And it works!

Two warnings to look into, in each master:

```
WARNING:ufo2ft.fontInfoData:Underline thickness not set in UFO, defaulting to UPM * 0.05
WARNING:ufo2ft.fontInfoData:Underline position not set in UFO, defaulting to UPM * -0.075
WARNING:ufo2ft.fontInfoData:Underline thickness not set in UFO, defaulting to UPM * 0.05
```

```
WARNING:ufo2ft.featureWriters.markFeatureWriter.MarkFeatureWriter:duplicate anchor 'above' in glyph 'aogonek.alt'
WARNING:ufo2ft.featureWriters.markFeatureWriter.MarkFeatureWriter:duplicate anchor 'below' in glyph 'aogonek.alt'
```

- [ ] set underline & strikethrough values (probably, these should be the same between all fonts, because software seems to only take one value for variable fonts, in my recent experience)
- [ ] check for duplicate anchors in 'aogonek.alt'

![GIF of working variable font for Tilt Warp](assets/Kapture 2020-01-31 at 18.43.53.gif)


**Questions for Andy:**
- Do you happen to have a guess at how RoboFont batch can build VFs if FontMake can't? Is it making OTFs, or somehow auto-fixing segments?
- Check that you are trying to build from the correct designspace files.
  -  `sources/Tilt Neon/Rotated/Tilt-Neon.designspace`
  -  `sources/Tilt Prism/Rotated 03 Combined/Tilt-Prism.designspace`
  -  `sources/Tilt Warp/Rotated/Tilt-Warp.designspace`

*(Pause at 18:45)*

---

*(Start at 21:30, Feb 2)*

```
INFO:ufo2ft:Pre-processing glyphs
ERROR:cu2qu.ufo:Glyphs named 'caron' have different number of segments
ERROR:cu2qu.ufo:Glyphs named 'cedilla' have different number of segments
ERROR:cu2qu.ufo:Glyphs named 'circumflex' have different number of segments
Traceback (most recent call last):
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/bin/fontmake", line 10, in <module>
    sys.exit(main())
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/fontmake/__main__.py", line 434, in main
    project.run_from_designspace(designspace_path, **args)
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/fontmake/font_project.py", line 884, in run_from_designspace
    **kwargs,
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/fontmake/font_project.py", line 950, in _run_from_designspace_interpolatable
    designspace, output_path=output_path, output_dir=output_dir, **kwargs
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/fontmake/font_project.py", line 305, in build_variable_font
    inplace=True,
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/ufo2ft/__init__.py", line 571, in compileVariableTTF
    debugFeatureFile=debugFeatureFile,
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/ufo2ft/__init__.py", line 398, in compileInterpolatableTTFsFromDS
    for source, ttf in zip(result.sources, ttfs):
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/ufo2ft/__init__.py", line 279, in compileInterpolatableTTFs
    glyphSets = preProcessor.process()
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/ufo2ft/preProcessor.py", line 220, in process
    remember_curve_type=self._rememberCurveType and self.inplace,
  File "/Users/stephennixon/type-repos/google-font-repos/Tilt-Typeface/venv/lib/python3.7/site-packages/cu2qu/ufo.py", line 295, in fonts_to_quadratic
    raise IncompatibleFontsError(glyph_errors)
cu2qu.errors.IncompatibleFontsError: fonts contains incompatible glyphs: x
```

Checking:

```
Segment types: 🥐 = curve | 📏 = line | 🚚 = move | 🥨 = qcurve

FONT                            | /caron: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | ****
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /cedilla: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 10] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 🥐 🥐 🥐  | 


FONT                            | /circumflex: contours & segments
------------------------------- | ------------------------------------------------------------------------------------------------
Source-HROTd_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTn.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTd_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
Source-HROTn_VROTd.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTn.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTn_VROTx.ufo          | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTd.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTn.ufo          | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
Source-HROTx_VROTx.ufo          | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTd_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTdd.ufo     | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTn.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTdd_VROTx.ufo      | C00 [segs 08] 🥐 🥐 🥐 🥐 🥐 📏 🥐 🥐  | 
SubSource-HROTn_VROTdd.ufo      | C00 [segs 06] 🥐 🥐 🥐 🥐 🥐 🥐  | 
SubSource-HROTx_VROTdd.ufo      | C00 [segs 08] 🥐 📏 🥐 🥐 🥐 🥐 🥐 🥐  | 
```


...I wonder whether I should bring over the "varfontprep" script from Recursive. I suspect these problems may persist... but then again, if the sources are *mostly* clean, maybe they should just get totally cleaned.

![](assets/2020-02-02-21-48-13.png)

Oh. Dear. This is a tricky interpolation to grock.

![](assets/2020-02-02-21-50-36.png)

I think this makes it compatible (at least it does according to a segment check), but it's hard to be confident that it will look precisely as intended. To get here, I just deleted the two extra points that led to very-short segments.

I see that the caron and circumflex appear to be the same shape, rotated 180 degrees. 

But also, reading Andy's emails again, I see that I'm working on the wrong thing: "You caught me in the middle of reworking a lot of glyphs, hold off on trying to build this one until I give you the go-ahead." 

I'm also seeing that in saving a change in `sources/Tilt Neon/Rotated/Source-HROTx_VROTx.ufo`, I modified *all* glyph files inside it; probably due to UFOnormalizer. I don't want to commit 1K+ changes or cause a git conflict later, so I'll git reset those files.


Okay; onto the Prism build instead.

Nice! Prism did indeed get fixed, and now builds on the first try.

*(moving to sparse build test, 22:00, feb 2)*