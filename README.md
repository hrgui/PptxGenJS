[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/ellerbrock/open-source-badge/) [![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php) [![npm version](https://badge.fury.io/js/pptxgenjs.svg)](https://badge.fury.io/js/pptxgenjs)

# PptxGenJS

### JavaScript framework that produces PowerPoint (pptx) presentations

Quickly and easily produce PowerPoint presentations with a few simple JavaScript commands in client web browsers or Node desktop apps.

## Main Features
* Complete JavaScript framework: No client configuration, plug-ins, or other settings required
* Works with all current desktop browsers (Chrome, Edge, Firefox, Opera et al.) and with IE11
* Full Featured: Create Tables, Shapes, Images, Text and Media - plus use Master Slides
* Presentation exports download to any modern browser as a normal PPTX file

## Additional Features
This framework also includes a unique [Table-to-Slides](#table-to-slides--1-click-exports) feature that will reproduce
an HTML Table across one or more Slides with a single command.

**************************************************************************************************

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  (*generated with [DocToc](https://github.com/thlorenz/doctoc)*)

- [Live Demo](#live-demo)
- [Installation](#installation)
  - [Client-Side](#client-side)
  - [Node.js (4.x)](#nodejs-4x)
- [Optional Library Files](#optional-library-files)
- [Presentation Basics](#presentation-basics)
- [Library Reference](#library-reference)
  - [Creating Presentations](#creating-presentations)
    - [Presentation Options](#presentation-options)
    - [Presentation Layouts](#presentation-layouts)
  - [Creating Slides](#creating-slides)
    - [Slide Options](#slide-options)
    - [Slide Number Options](#slide-number-options)
  - [Adding Text](#adding-text)
    - [Text Options](#text-options)
    - [Text Examples](#text-examples)
  - [Adding Tables](#adding-tables)
    - [Table Layout Options](#table-layout-options)
    - [Table Formatting Options](#table-formatting-options)
    - [Table Cell Formatting](#table-cell-formatting)
    - [Table Cell Formatting Examples](#table-cell-formatting-examples)
    - [Table Examples](#table-examples)
  - [Adding Shapes](#adding-shapes)
    - [Shape Options](#shape-options)
    - [Shape Examples](#shape-examples)
  - [Adding Images](#adding-images)
    - [Image Options](#image-options)
    - [Image Examples](#image-examples)
  - [Adding Media (Audio/Video/YouTube)](#adding-media-audiovideoyoutube)
    - [Media Options](#media-options)
    - [Media Examples](#media-examples)
- [Master Slides and Corporate Branding](#master-slides-and-corporate-branding)
  - [Slide Masters](#slide-masters)
  - [Slide Master Examples](#slide-master-examples)
  - [Slide Master Object Options](#slide-master-object-options)
  - [Sample Slide Master File](#sample-slide-master-file)
- [Table-to-Slides Feature](#table-to-slides-feature)
    - [Table-to-Slides Options](#table-to-slides-options)
    - [Notes:](#notes)
    - [Table-to-Slides Example](#table-to-slides-example)
  - [Master Pages and Branding](#master-pages-and-branding)
  - [Override Slide Master Settings](#override-slide-master-settings)
  - [One-Line Presentation Exports](#one-line-presentation-exports)
    - [Easy SharePoint Integration](#easy-sharepoint-integration)
- [Performance Considerations](#performance-considerations)
  - [Pre-Encode Large Images](#pre-encode-large-images)
- [Issues / Suggestions](#issues--suggestions)
- [Development Roadmap](#development-roadmap)
- [Special Thanks](#special-thanks)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

**************************************************************************************************
# Live Demo
Use JavaScript to Create a PowerPoint presentation with your web browser right now:  
[http://gitbrent.github.io/PptxGenJS](http://gitbrent.github.io/PptxGenJS)

# Installation
## Client-Side
PptxGenJS requires only three additional JavaScript libraries to function.
```javascript
<script lang="javascript" src="PptxGenJS/libs/jquery.min.js"></script>
<script lang="javascript" src="PptxGenJS/libs/jszip.min.js"></script>
<script lang="javascript" src="PptxGenJS/libs/filesaver.min.js"></script>
<script lang="javascript" src="PptxGenJS/dist/pptxgen.js"></script>
```
## Node.js (4.x)
[PptxGenJS NPM Homepage](https://www.npmjs.com/package/pptxgenjs)
```javascript
npm install pptxgenjs

var pptx = require("pptxgenjs");
```

# Optional Library Files
If you are planning on creating Shapes (basically anything other than Text, Tables or Rectangles), then you'll want to
include the `pptxgen.shapes.js` library.  It's a complete PowerPoint PPTX Shape object array thanks to the
[officegen project](https://github.com/Ziv-Barber/officegen)
```javascript
<script lang="javascript" src="PptxGenJS/dist/pptxgen.shapes.js"></script>
```

**************************************************************************************************
# Presentation Basics
PowerPoint Presentations are created via JavaScript by following 4 basic steps:

1. Create the Presentation
2. Add a new Slide  
3. Add objects (Images, Shapes, Text or Tables)
4. Save the Presentation  

```javascript
var pptx = new PptxGenJS();
var slide = pptx.addNewSlide();
slide.addText('Hello World!', { x:1.5, y:1.5, font_size:18, color:'363636' });
pptx.save('Sample Presentation');
```
That's really all there is to it!

**************************************************************************************************
# Library Reference

## Creating Presentations

Client Browser:
```javascript
var pptx = new PptxGenJS();
```
Node.js:
```javascript
var pptx = require("pptxgenjs");
```

### Presentation Options
Setting the Title:
```javascript
pptx.setTitle('PptxGenJS Sample Presentation');
```
Setting the Layout (applies to all Slides in the Presentation):
```javascript
pptx.setLayout('LAYOUT_WIDE');
```

### Presentation Layouts
| Layout Name    | Default  | Layout Slide Size |
| :------------- | :------- | :---------------- |
| `LAYOUT_16x9`  | Yes      | 10 x 5.625 inches |
| `LAYOUT_16x10` | No       | 10 x 6.25 inches  |
| `LAYOUT_4x3`   | No       | 10 x 7.5 inches   |
| `LAYOUT_WIDE`  | No       | 13.3 x 7.5 inches |

## Creating Slides

Add a Slide to a Presentation
```javascript
var slide = pptx.addNewSlide();
```

### Slide Options
Applying Master Slides
```javascript
var slide = pptx.addNewSlide(pptx.masters.TITLE_SLIDE);
```
Adding Slide Numbers
```javascript
slide.slideNumber({ x:1.0, y:'90%' });
```

### Slide Number Options
| Option       | Type    | Unit   | Default   | Description         | Possible Values  |
| :----------- | :------ | :----- | :-------- | :------------------ | :--------------- |
| `x`          | number  | inches | `0.3`     | horizontal location | 0-n OR 'n%'. (Ex: `{x:'10%'}` places number 10% from left edge) |
| `y`          | number  | inches | `90%`     | vertical location   | 0-n OR 'n%'. (Ex: `{y:'90%'}` places number 90% down the Slide) |

## Adding Text
```javascript
// Syntax
slide.addText('TEXT', {OPTIONS});

// Example
slide.addText('Hello World!', { x:2, y:3, color:'DDDD00', font_size:90 });
slide.addText('Text Options', { x:2, y:4, font_face:'Arial', font_size:42, color:'00CC00', bold:true, italic:true, underline:true } );
```

### Text Options
| Option       | Type    | Unit   | Default   | Description         | Possible Values  |
| :----------- | :------ | :----- | :-------- | :------------------ | :--------------- |
| `x`          | number  | inches | `1.0`     | horizontal location | 0-n OR 'n%'. (Ex: `{x:'50%'}` will place object in the middle of the Slide) |
| `y`          | number  | inches | `1.0`     | vertical location   | 0-n OR 'n%'. |
| `w`          | number  | inches |           | width               | 0-n OR 'n%'. (Ex: `{w:'50%'}` will make object 50% width of the Slide) |
| `h`          | number  | inches |           | height              | 0-n OR 'n%'. |
| `align`      | string  |        | `left`    | alignment           | `left` or `center` or `right` |
| `autoFit`    | boolean |        | `false`   | "Fit to Shape"      | `true` or `false` |
| `bold`       | boolean |        | `false`   | bold text           | `true` or `false` |
| `bullet`     | boolean |        | `false`   | bulleted text       | `true` or `false` |
| `color`      | string  |        |           | text color          | hex color code. Ex: `{ color:'0088CC' }` |
| `fill`       | string  |        |           | fill/bkgd color     | hex color code. Ex: `{ color:'0088CC' }` |
| `font_face`  | string  |        |           | font face           | Ex: 'Arial' |
| `font_size`  | number  | points |           | font size           | 1-256. Ex: `{ font_size:12 }` |
| `inset`      | number  | inches |           | inset/padding       | 1-256. Ex: `{ inset:1.25 }` |
| `isTextBox`  | boolean |        | `false`   | PPT "Textbox"       | `true` or `false` |
| `italic`     | boolean |        | `false`   | italic text         | `true` or `false` |
| `margin`     | number  | points |           | margin              | 1-n (ProTip: use the same value from CSS padding) |
| `underline`  | boolean |        | `false`   | underline text      | `true` or `false` |
| `valign`     | string  |        |           | vertical alignment  | `top` or `middle` or `bottom` |

### Text Examples
```javascript
var pptx = new PptxGenJS();
var slide = pptx.addNewSlide();

slide.addText('Hello',  { x:0.5, y:0.7, w:3, color:'0000FF', font_size:64 });
slide.addText('World!', { x:2.7, y:1.0, w:5, color:'DDDD00', font_size:90 });
slide.addText('^ (50%/50%)', {x:'50%', y:'50%'});
var objOptions = {
    x:0.5, y:4.3, w:'90%',
    font_face:'Arial', font_size:32, color:'00CC00', bold:true, underline:true, margin:0, isTextBox:true
};
slide.addText('Arial, 32pt, green, bold, underline, 0 inset', objOptions);

pptx.save('Demo-Text');
```

## Adding Tables
Syntax:
```javascript
slide.addTable( [rows] );
slide.addTable( [rows], {any Layout/Formatting OPTIONS} );
```

### Table Layout Options
| Option       | Type    | Unit   | Default   | Description         | Possible Values  |
| :----------- | :------ | :----- | :-------- | :------------------ | :--------------- |
| `x`          | number  | inches | `1.0`     | horizontal location | 0-n OR 'n%'. (Ex: `{x:'50%'}` will place object in the middle of the Slide) |
| `y`          | number  | inches | `1.0`     | vertical location   | 0-n OR 'n%'. |
| `w`          | number  | inches |           | width               | 0-n OR 'n%'. (Ex: `{w:'50%'}` will make object 50% width of the Slide) |
| `h`          | number  | inches |           | height              | 0-n OR 'n%'. |
| `colW`       | integer | inches |           | width for every column | Ex: Width for every column in table (uniform) `2.0` |
| `colW`       | array   | inches |           | column widths in order | Ex: Width for each of 5 columns `[1.0, 2.0, 2.5, 1.5, 1.0]` |
| `rowH`       | integer | inches |           | height for every row   | Ex: Height for every row in table (uniform) `2.0` |
| `rowH`       | array   | inches |           | row heights in order   | Ex: Height for each of 5 rows `[1.0, 2.0, 2.5, 1.5, 1.0]` |

### Table Formatting Options
| Option       | Type    | Unit   | Default   | Description        | Possible Values  |
| :----------- | :------ | :----- | :-------- | :----------------- | :--------------- |
| `align`      | string  |        | `left`    | alignment          | `left` or `center` or `right` (or `l` `c` `r`) |
| `bold`       | boolean |        | `false`   | bold text          | `true` or `false` |
| `border`     | object  |        |           | cell border        | object with `pt` and `color` values. Ex: `{pt:'1', color:'f1f1f1'}` |
| `border`     | array   |        |           | cell border        | array of objects with `pt` and `color` values in TRBL order. |
| `color`      | string  |        |           | text color         | hex color code. Ex: `{color:'0088CC'}` |
| `colspan`    | integer |        |           | column span        | 2-n. Ex: `{colspan:2}` |
| `fill`       | string  |        |           | fill/bkgd color    | hex color code. Ex: `{color:'0088CC'}` |
| `font_face`  | string  |        |           | font face          | Ex: 'Arial' |
| `font_size`  | number  | points |           | font size          | 1-256. Ex: `{font_size:12}` |
| `italic`     | boolean |        | `false`   | italic text        | `true` or `false` |
| `marginPt`   | number  | points |           | margin             | 1-n (ProTip: use the same value from CSS padding) |
| `rowspan`    | integer |        |           | row span           | 2-n. Ex: `{rowspan:2}` |
| `underline`  | boolean |        | `false`   | underline text     | `true` or `false` |
| `valign`     | string  |        |           | vertical alignment | `top` or `middle` or `bottom` (or `t` `m` `b`) |

### Table Cell Formatting
* **Formatting Options** passed to `slide.addTable()` apply to every cell in the table
* You can selectively override formatting on a per-cell basis by including any **Formatting Option** in the row cell itself

### Table Cell Formatting Examples
```javascript
var rows = [];
// These cells will be formatted according to any options provided to addTable()
rows.push( ['First', 'Second', 'Third'] );
// Any formatting options provided by cells will be applied - overriding table options (if any)
rwos.push([
    { text:'1st', opts:{color:'ff0000'} },
    { text:'2nd', opts:{color:'00ff00'} },
    { text:'3rd', opts:{color:'0000ff'} }
]);
```

### Table Examples
```javascript
var pptx = new PptxGenJS();
var slide = pptx.addNewSlide();
slide.addText('Demo-03: Table', { x:0.5, y:0.25, font_size:18, font_face:'Arial', color:'0088CC' });

// TABLE 1: Single-row table
// --------
var rows = [ 'Cell 1', 'Cell 2', 'Cell 3' ];
var tabOpts = { x:0.5, y:1.0, w:9.0, fill:'F7F7F7', font_size:14, color:'363636' };
slide.addTable( rows, tabOpts );

// TABLE 2: Multi-row table (each rows array element is an array of cells)
// --------
var rows = [
    ['A1', 'B1', 'C1'],
    ['A2', 'B2', 'C2']
];
var tabOpts = { x:0.5, y:2.0, w:9.0, fill:'F7F7F7', font_size:18, color:'6f9fc9' };
slide.addTable( rows, tabOpts );

// TABLE 3: Formatting at a cell level - use this to selectively override table's cell options
// --------
var rows = [
    [
        { text:'Top Lft', opts:{ valign:'t', align:'l', font_face:'Arial'   } },
        { text:'Top Ctr', opts:{ valign:'t', align:'c', font_face:'Verdana' } },
        { text:'Top Rgt', opts:{ valign:'t', align:'r', font_face:'Courier' } }
    ],
];
var tabOpts = { x:0.5, y:4.5, w:9.0, fill:'F7F7F7', font_size:18, color:'6f9fc9', rowH:0.6, valign:'m'} };
slide.addTable( rows, tabOpts );

pptx.save('Demo-Tables');
```

## Adding Shapes
Syntax (no text):
```javascript
slide.addShape({SHAPE}, {OPTIONS});
```
Syntax (with text):
```javascript
slide.addText("some string", {SHAPE, OPTIONS});
```
Check the `pptxgen.shapes.js` file for a complete list of the hundreds of PowerPoint shapes available.

### Shape Options
| Option       | Type    | Unit   | Default   | Description         | Possible Values  |
| :----------- | :------ | :----- | :-------- | :------------------ | :--------------- |
| `x`          | number  | inches | `1.0`     | horizontal location | 0-n OR 'n%'. (Ex: `{x:'50%'}` will place object in the middle of the Slide) |
| `y`          | number  | inches | `1.0`     | vertical location   | 0-n OR 'n%'. |
| `w`          | number  | inches |           | width               | 0-n OR 'n%'. (Ex: `{w:'50%'}` will make object 50% width of the Slide) |
| `h`          | number  | inches |           | height              | 0-n OR 'n%'. |
| `align`      | string  |        | `left`    | alignment           | `left` or `center` or `right` |
| `fill`       | string  |        |           | fill/bkgd color     | hex color code. Ex: `{color:'0088CC'}` |
| `fill`       | object |   |   | fill/bkgd color | object with `type`, `color` and optional `alpha` keys. Ex: `fill:{type:'solid', color:'0088CC', alpha:25}` |
| `flipH`      | boolean |        |           | flip Horizontal     | `true` or `false` |
| `flipV`      | boolean |        |           | flip Vertical       | `true` or `false` |
| `line`       | string  |        |           | border line color   | hex color code. Ex: `{line:'0088CC'}` |
| `line_head`  | string  |        |           | border line ending  | `arrow`, `diamond`, `oval`, `stealth`, `triangle` or `none` |
| `line_size`  | number  | points |           | border line size    | 1-256. Ex: {line_size:4} |
| `line_tail`  | string  |        |           | border line heading | `arrow`, `diamond`, `oval`, `stealth`, `triangle` or `none` |
| `rotate`     | integer | degrees |          | rotation degrees    | 0-360. Ex: `{rotate:180}` |

### Shape Examples
```javascript
var pptx = new PptxGenJS();
pptx.setLayout('LAYOUT_WIDE');

var slide = pptx.addNewSlide();

// Misc Shapes
slide.addShape(pptx.shapes.LINE,      { x:4.15, y:4.40, w:5, h:0, line:'FF0000', line_size:1 });
slide.addShape(pptx.shapes.LINE,      { x:4.15, y:4.80, w:5, h:0, line:'FF0000', line_size:2, line_head:'triangle' });
slide.addShape(pptx.shapes.LINE,      { x:4.15, y:5.20, w:5, h:0, line:'FF0000', line_size:3, line_tail:'triangle' });
slide.addShape(pptx.shapes.LINE,      { x:4.15, y:5.60, w:5, h:0, line:'FF0000', line_size:4, line_head:'triangle', line_tail:'triangle' });
slide.addShape(pptx.shapes.RECTANGLE, { x:0.50, y:0.75, w:5, h:3, fill:'FF0000' });
slide.addShape(pptx.shapes.OVAL,      { x:4.15, y:0.75, w:5, h:2, fill:{ type:'solid', color:'0088CC', alpha:25 } });

// Adding text to Shapes:
slide.addText('RIGHT-TRIANGLE', { shape:pptx.shapes.RIGHT_TRIANGLE, align:'c', x:0.40, y:4.3, w:6, h:3, fill:'0088CC', line:'000000', line_size:3 });
slide.addText('RIGHT-TRIANGLE', { shape:pptx.shapes.RIGHT_TRIANGLE, align:'c', x:7.00, y:4.3, w:6, h:3, fill:'0088CC', line:'000000', flipH:true });

pptx.save('Demo-Shapes');
```


## Adding Images
Syntax:
```javascript
slide.addImage({OPTIONS});
```

Animated GIFs can be included in Presentations in one of two ways:
* Using Node.js: use either `data` or `path` options (Node can encode any image into base64)
* Client Browsers: pre-encode the gif and add it using the `data` option (encoding images into GIFs is beyond any current browser)

### Image Options
| Option       | Type    | Unit   | Default   | Description         | Possible Values  |
| :----------- | :------ | :----- | :-------- | :------------------ | :--------------- |
| `x`          | number  | inches | `1.0`     | horizontal location | 0-n |
| `y`          | number  | inches | `1.0`     | vertical location   | 0-n |
| `w`          | number  | inches | `1.0`     | width               | 0-n |
| `h`          | number  | inches | `1.0`     | height              | 0-n |
| `data`       | string  |        |           | image data (base64) | base64-encoded image string. (either `data` or `path` is required) |
| `path`       | string  |        |           | image path          | Same as used in an (img src="") tag. (either `data` or `path` is required) |

**Deprecation Warning**
Old positional parameters (e.g.: `slide.addImage('images/chart.png', 1, 1, 6, 3)`) are now deprecated as of 1.1.0

### Image Examples
```javascript
var pptx = new PptxGenJS();
var slide = pptx.addNewSlide();

// Image by path
slide.addImage({ path:'images/chart_world_peace_near.png', x:1.0, y:1.0, w:8.0, h:4.0 });
// Image by data (base64-encoding)
slide.addImage({ data:'image/png;base64,iVtDafDrBF[...]=', x:3.0, y:5.0, w:6.0, h:3.0 });

// NOTE: Slide API calls return the same slide, so you can chain calls:
slide.addImage({ path:'images/cc_license_comp_chart.png', x:6.6, y:0.75, w:6.30, h:3.70 })
     .addImage({ path:'images/cc_logo.jpg',               x:0.5, y:3.50, w:5.00, h:3.70 })
     .addImage({ path:'images/cc_symbols_trans.png',      x:6.6, y:4.80, w:6.30, h:2.30 });

pptx.save('Demo-Images');
```

## Adding Media (Audio/Video/YouTube)
Syntax:
```javascript
slide.addMedia({OPTIONS});
```

Both Video (mpg, mov, mp4, m4v, etc.) and Audio (mp3, wav, etc.) are supported (list of [supported formats](https://support.office.com/en-us/article/Video-and-audio-file-formats-supported-in-PowerPoint-d8b12450-26db-4c7b-a5c1-593d3418fb59#OperatingSystem=Windows))
* Using Node.js: use either `data` or `path` options (Node can encode any media into base64)
* Client Browsers: pre-encode the media and add it using the `data` option (encoding video/audio is beyond any current browser)

Online video (YouTube embeds, etc.) is supported in both client browser and in Node.js

### Media Options
| Option       | Type    | Unit   | Default   | Description         | Possible Values  |
| :----------- | :------ | :----- | :-------- | :------------------ | :--------------- |
| `x`          | number  | inches | `1.0`     | horizontal location | 0-n |
| `y`          | number  | inches | `1.0`     | vertical location   | 0-n |
| `w`          | number  | inches | `1.0`     | width               | 0-n |
| `h`          | number  | inches | `1.0`     | height              | 0-n |
| `data`       | string  |        |           | media data (base64) | base64-encoded string |
| `path`       | string  |        |           | media path          | relative path to media file |
| `link`       | string  |        |           | online url/link     | link to online video. Ex: `link:'https://www.youtube.com/embed/blahBlah'` |
| `type`       | string  |        |           | media type          | media type: `audio` or `video` (reqs: `data` or `path`) or `online` (reqs:`link`) |

### Media Examples
```javascript
var pptx = new PptxGenJS();
var slide = pptx.addNewSlide();

// Media by path (Node.js only)
slide.addMedia({ type:'audio', path:'../media/sample.mp3', x:1.0, y:1.0, w:3.0, h:0.5 });
// Media by data (client browser or Node.js)
slide.addMedia({ type:'audio', data:'audio/mp3;base64,iVtDafDrBF[...]=', x:3.0, y:1.0, w:6.0, h:3.0 });
// Online by link (client browser or Node.js)
slide.addMedia({ type:'online', link:'https://www.youtube.com/embed/Dph6ynRVyUc', x:1.0, y:4.0, w:8.0, h:4.5 });

pptx.save('Demo-Media');
```

**************************************************************************************************
# Master Slides and Corporate Branding

## Slide Masters
Generating sample slides like those shown above is great for demonstrating library features,
but the reality is most of us will be required to produce presentations that have a certain design or
corporate branding.

PptxGenJS allows you to define Master Slides via objects that can then be used to provide branding
functionality.

Slide Masters are defined using the same object style used in Slides. Add these objects as a variable to a file that
is included in the script src tags on your page, then reference them by name in your code.  
E.g.: `<script lang="javascript" src="pptxgenjs.masters.js"></script>`

## Slide Master Examples
`pptxgenjs.masters.js` contents:
```javascript
var gObjPptxMasters = {
  MASTER_SLIDE: {
    title:  'Slide master',
    margin: [ 0.5, 0.25, 1.0, 0.25 ],
    bkgd:   'FFFFFF',
    images: [ { path:'images/logo_square.png', x:9.3, y:4.9, w:0.5, h:0.5 } ],
    shapes: [
      { type:'text', text:'ACME - Confidential', x:0, y:5.17, w:'100%', h:0.3, align:'center', valign:'top', color:'7F7F7F', font_size:8, bold:true },
      { type:'line', x:0.3, y:3.85, w:5.7, h:0.0, line:'007AAA' },
      { type:'rectangle', x:0, y:0, w:'100%', h:.65, w:5, h:3.2, fill:'003b75' }
    ],
    slideNumber: { x:0.3, y:'90%' }
  },
  TITLE_SLIDE: {
    title:  'I am the Title Slide',
    bkgd:   { data:'image/png;base64,R0lGONlhotPQBMAPyoAPosR[...]+0pEZbEhAAOw==' },
    images: [ { x:'7.4', y:'4.1', w:'2', h:'1', data:'image/png;base64,R0lGODlhPQBEAPeoAJosM[...]+0pCZbEhAAOw==' } ]
  }
};
```  
Every object added to the global master slide variable `gObjPptxMasters` can then be referenced
by their key names that you created (e.g.: "TITLE_SLIDE").  

**TIP:**
Pre-encode your images (base64) and add the string as the optional data key/val
(see the `TITLE_SLIDE.images` object above)

```javascript
var pptx = new PptxGenJS();

var slide1 = pptx.addNewSlide( pptx.masters.TITLE_SLIDE );
slide1.addText('How To Create PowerPoint Presentations with JavaScript', { x:0.5, y:0.7, font_size:18 });
// NOTE: Base master slide properties can be overridden on a selective basis:
// Here we can set a new background color or image on-the-fly
var slide2 = pptx.addNewSlide( pptx.masters.MASTER_SLIDE, { bkgd:'0088CC' } );
var slide3 = pptx.addNewSlide( pptx.masters.MASTER_SLIDE, { bkgd:{ path:'images/title_bkgd.jpg' } } );
var slide4 = pptx.addNewSlide( pptx.masters.MASTER_SLIDE, { bkgd:{ data:'image/png;base64,tFfInmP[...]=' } } );

pptx.save();
```

## Slide Master Object Options
| Option        | Type    | Unit   | Default  | Description  | Possible Values       |
| :------------ | :------ | :----- | :------- | :----------- | :-------------------- |
| `bkgd`        | string  |        | `ffffff` | color        | hex color code. Ex: `{ bkgd:'0088CC' }` |
| `bkgd`        | object  |        |          | image | object with path OR data. Ex: `{path:'img/bkgd.png'}` OR `{data:'image/png;base64,iVBORwTwB[...]='}` |
| `images`      | array   |        |   | image(s) | object array of path OR data. Ex: `{path:'img/logo.png'}` OR `{data:'image/png;base64,tFfInmP[...]'}`|
| `slideNumber` | object  |        |          | Show slide numbers | ex: `{ x:1.0, y:'50%' }` `x` and `y` can be either inches or percent |
| `margin`      | number  | inches | `1.0`    | Slide margin       | 0.0 through whatever |
| `margin`      | array   |        |          | Slide margins      | array of numbers in TRBL order. Ex: `[0.5, 0.75, 0.5, 0.75]` |
| `shapes`      | array   |        |          | shape(s)           | array of shape objects. Ex: (see [Shape](#shape) section) |
| `title`       | string  |        |          | Slide title        | some title |

## Sample Slide Master File
A sample masters file is included in the distribution folder and contain a couple of different slides to get you started.  
Location: `PptxGenJS/dist/pptxgen.masters.js`

**************************************************************************************************
# Table-to-Slides Feature
* With the unique `addSlidesForTable()` function, you can reproduce an HTML table - background
colors, borders, fonts, padding, etc. - with a single line of code.
* The function will detect margins (based on Master Slide layout or parameters) and will create Slides as needed
* All you have to do is pass the table element ID to `addSlidesForTable()` and you're done!
* NOTE: Nested tables are not supported in PowerPoint

### Table-to-Slides Options
| Option       | Type    | Unit   | Default   | Description         | Possible Values  |
| :----------- | :------ | :----- | :-------- | :------------------ | :--------------- |
| `x`          | number  | inches |           | horizontal location | 0-n |
| `y`          | number  | inches |           | vertical location   | 0-n |
| `w`          | number  | inches |           | width               | 0-n |
| `h`          | number  | inches |           | height              | 0-n |

### Notes:
* Default margins are 0.5 inches, table will take up all remaining space by default
* Use a Master Slide with pre-defined margins to over-ride defaults

### Table-to-Slides Example
```javascript
// STEP 1: Instantiate new PptxGenJS instance
var pptx = new PptxGenJS();

// STEP 2: Set slide size/layout
pptx.setLayout('LAYOUT_16x9');

// STEP 3: Pass table element ID to addSlidesForTable function to produce 1-N slides
pptx.addSlidesForTable('tabAutoPaging');

// STEP 4: Export Presentation
pptx.save('Table2SlidesDemo');
```

## Master Pages and Branding
Do you need to have the generated slides use a Slide Master or corporate branding?  
Just pass the Slide Master name to use (you can also add shapes/text on-the-fly as well).

## Override Slide Master Settings
The Master Slide background color/image can be selectively overridden on a per-slide basis when needed,
so it's easy to handle exceptions where users want things like the first slide to have a white background, etc.
```javascript
var slide1 = pptx.addNewSlide( pptx.masters.MASTER_SLIDE, { bkgd:'0088CC'} );
```

## One-Line Presentation Exports
Your Slide Master should already contain slide layout, size & margins. Meaning, the code to produce
professional looking slides is so small that you can just inline it into a button and place next to any table on your site:

```javascript
<input type="button" value="Export to PPTX" onclick="{ var pptx = new PptxGenJS(); pptx.addSlidesForTable('tableId',{ master:pptx.masters.MASTER_SLIDE }); pptx.save(); }">
```

### Easy SharePoint Integration
Placing a button like this into a WebPart is a great way to add "Export to PowerPoint" functionality
to SharePoint. (You'd also need to add the 4 `<script>` includes in the same or another WebPart)

**************************************************************************************************
# Performance Considerations
It takes CPU time to read and encode images! The more images you include and the larger they are, the more time will be consumed.
The time needed to read/encode images can be completely eliminated by pre-encoding any images (see below).

## Pre-Encode Large Images
Pre-encode images into a base64 string (eg: 'image/png;base64,iVBORw[...]=') for use as the `data` option value.
This will both reduce dependencies (who needs another image asset to keep track of?) and provide a performance
boost (no time will need to be consumed reading and encoding the image).

**************************************************************************************************
# Issues / Suggestions

Please file issues or suggestions on the [issues page on github](https://github.com/gitbrent/PptxGenJS/issues/new), or even better, [submit a pull request](https://github.com/gitbrent/PptxGenJS/pulls). Feedback is always welcome!

When reporting issues, please include a code snippet or a link demonstrating the problem.
Here is a small [jsFiddle](https://jsfiddle.net/gitbrent/gx34jy59/5/) that is already configured and uses the latest PptxGenJS code.

**************************************************************************************************
# Development Roadmap

Version 2.0 will be released later in 2017 and will drop support for IE11 as we move to adopt more
JavaScript ES6 features and remove many instances of jQuery utility functions.

**************************************************************************************************
# Special Thanks

* [Officegen Project](https://github.com/Ziv-Barber/officegen) - For the Shape definitions and XML code
* [Dzmitry Dulko](https://github.com/DzmitryDulko) - For getting the project published on NPM
* Everyone who has submitted a Issue or a Pull Request. :-)

**************************************************************************************************
# License

Copyright &copy; 2015-2017 [Brent Ely](https://github.com/gitbrent/PptxGenJS)

[MIT](https://github.com/gitbrent/PptxGenJS/blob/master/LICENSE)
