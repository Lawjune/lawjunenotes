# Getting Started

**We'll learn**

- Layouts
- Typography
- Images
- Forms
- Transformation
- Animations

moshified.com

# Layout

- CSS Box model
- Sizing elements
- Overflowing
- Measurement units
- Positioning
- Floating elements
- FlexBox & Grid layouts
- Media queries

## The Box Model

Margin>Border>Padding>Content

```HTML
    <p>Lorem ipsum dolor sit amet.</p>
    <p>Lorem ipsum dolor sit amet.</p>
```

```CSS
p {
  padding: 20px; /* vertical horizontal */
  margin: 0; /*over-lapped*/
}
```

Use the margin property to separate elements and the padding property to add space between the border and the content area of element.

## Sizing Elements

```HTML
    <div class="box"></div>
```

```CSS
.box {
  width: 100px;
  height: 100px;
  background-color: gold;
  padding: 20px;
  border: 10px solid orange;
  margin: 20px;
}
```

By default:

- The width and height are applied to the content area.
- The padding will increase the size of the visible box.
- The margin property will not increase the size of the visible box, which move the box from the original position.

Caculating the actual size of an element and get a little bit complex, this is where the box-sizing property comes to the rescue.

```CSS
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 10px;
}

.box::before {
  content: "Hello";
}

.box {
  width: 100px;
  height: 100px;
  background-color: gold;
}
```

<div> is a block element, which will cover the entire horizental area.

<span> is an inline element.

```HTML
    <span class="box"></span>
    <span class="box"></span>
```

```CSS
.box {
  width: 100px;
  height: 100px;
  background-color: gold;
  display: inline-block;
}
```

To get rid of the little space between two <span>

```HTML
<span class="box"></span><span class="box"></span>
```

## Overflowing

```HTML
    <div class="box">
      <p>
        Lorem200
      </p>
    </div>
```

```CSS
.box {
  border: 3px solid gold;
  width: 150px;
  height: 150px;
  overflow: auto;
}
```

## Measurement Units

- **ABSOLUTE**

  - px
  - pt
  - in
  - cm
  - mm

```CSS
  .box {
  width: 100px;
  height: 100px;
  background-color: gold;
  border-top: 3px solid orange;
}
```

- **RELATIVE**
  - % | relative to the size of the container
  - vw |
    | relative to the viewpoint
  - vh |
  - em |
    | relative to the font size
  - rem |

```CSS
  .box {
  /* 50% of the width of parent */
  /* width: 50% */
  width: 50vw;
  height: 100vh;
  background-color: gold;
  border-top: 3px solid orange;
}
```

```CSS
.box {
  /* 10 x font size of the current element */
  /* 10 x 16px as default base font size */
  width: 10em;
  ...
```

```CSS
.box {
  /* 10 x font size of the root element */
  width: 10rem;
  ...
}
```

```CSS
html {
  /* 62.5% of 16px = 10px*/
  font-size: 62.5%;
}

body {
  margin: 10px;
}

.box {
  /* 10 x font size of the current element */
  /* 10 x 16px as default base font size */
  width: 10rem;
  height: 100vh;
  background-color: gold;
  border-top: 3px solid orange;
}
```

## Positioning

```HTML
    <div class="boxes">
      <div class="box box-one"></div>
      <div class="box box-two"></div>
      <div class="box box-three"></div>
    </div>
```

```CSS
html {
  /* 62.5% of 16px = 10px*/
  font-size: 62.5%;
}

body {
  margin: 10px;
}

.boxes {
  border: 3px solid lightgray;
  /* position: relative; */
}

.box {
  width: 5rem;
  height: 5rem;
}

.box-one {
  background-color: gold;
}

.box-two {
  background-color: tomato;
  position: absolute;
  left: 4rem;
  bottom: 4rem;
  z-index: -1;
}

.box-three {
  background-color: dodgerblue;
}
```

```CSS
html {
  /* 62.5% of 16px = 10px*/
  font-size: 62.5%;
}

body {
  margin: 10px;
}

.boxes {
  border: 3px solid lightgray;
  position: relative;
}

.box {
  width: 5rem;
  height: 5rem;
}

.box-one {
  background-color: gold;
}

.box-two {
  background-color: tomato;
  position: absolute;
  right: 0;
  bottom: 0;
  z-index: 999999;
}

.box-three {
  background-color: dodgerblue;
}
```

```CSS
.box-two {
  background-color: tomato;
  position: fixed;
  top: 0;
  z-index: 999999;
}
```

```CSS
.box-two {
  background-color: tomato;
  position: fixed;
  top: 0;
  left: 2rem;
  right: 2rem;
  width: auto;
  z-index: 999999;
}
```

**POSITIONING SUMMARY**

- **_Relative_**: relative to the element's normal position
- **_Absolute_**: relative to the parent
- **_Fixed_**: relative to the viewport

### Floating Elements

```HTML
  <body>
    <article class="tweet">
      <div class="avatar"></div>
      <p>Lorem ipsum dolor sit amet.</p>
      <p class="clear">
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. Ex et nam
        repudiandae est harum, nemo reiciendis quis, amet hic aliquam fugit,
        excepturi ad. Deleniti ut a temporibus eligendi tempore inventore itaque
        commodi ea labore at, maiores recusandae nesciunt saepe illo iste! Vitae
        voluptate eius aliquam accusantium doloribus eum praesentium odio
        numquam modi iusto excepturi adipisci nisi impedit earum rerum, cumque
        repellendus nemo, labore qui? Ab sit, voluptas nemo cumque id error,
        exercitationem mollitia odit repellat non distinctio suscipit quod quam?
      </p>
    </article>
  </body>
```

```CSS
.avatar {
  width: 5rem;
  height: 5rem;
  background-color: gold;
  float: left;
  margin-right: 10px;
}

.clear {
  clear: both;
}
```

Block floating over the box.

```HTML
  <body>
    <article class="tweet">
      <div class="avatar"></div>
    </article>
  </body>
```

Solution 1:

```HTML
    <article class="tweet">
      <div class="avatar"></div>
      <p>Lorem ipsum dolor sit amet.</p>
      <!-- Add a clear div to "clear" the floating -->
      <div class="clear"></div>
    </article>
```

Solution 2：

```HTML
    <article class="tweet clearfix">
      <div class="avatar"></div>
      <p>Lorem ipsum dolor sit amet.</p>
```

```CSS
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}
```

```CSS
.tweet {
  border: 3px solid lightgray;
  /* overflow: hidden; Do not use it!!!! */
}
```

### FlexBox

**Flexible Box Layout (FlexBox)**
Used for laying out elements in one direction

```HTML
    <div class="container">
      <div class="box">A</div>
      <div class="box">B</div>
      <div class="box">C</div>
    </div>
```

```CSS
.container {
  border: 3px solid lightgray;
  display: flex;
  flex-direction: row-reverse;
}

.box {
  width: 5rem;
  height: 5rem;
  background: gold;
  margin: 1rem;
}
```

#### Alignment

**AXES**

- Main (primary)
- Cross (secondary)

- **DIRECTION: ROW**

  - Main (primary) -> x
  - Cross (secondary) -> y

- **DIRECTION: COLUMN**
  - Main (primary) -> y
  - Cross (secondary) -> x

**ALIGNMENT ITEMS**

- justify-content (along the **main** axis)
- align-items (along the **cross** axis)
- align-content -> Used very little, only works for multiple lines in a container

```HTML
    <div class="container">
      <div class="box">A</div>
      <div class="box">B</div>
      <div class="box">C</div>
      <div class="box">E</div>
      <div class="box">F</div>
      <div class="box">G</div>
      <div class="box">H</div>
    </div>
```

```CSS
.container {
  border: 3px solid lightgray;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  align-content: center;
  height: 90vh;
}
```

```HTML
    <div class="container">
      <div class="box box-one">A</div>
      <div class="box">B</div>
      <div class="box">C</div>
    </div>
```

```CSS
.box-one {
  align-self: flex-start;
}
```

#### Sizing Items

- flex-basis (the initial size of flex item)
- flex-grow (the growth factor)
- flex-shrink (the shrink factor)
- flex

```CSS
.box {
  flex-basis: 10rem;
  width: 5rem;
  height: 5rem;
  background: gold;
  margin: 1rem;
}

.box-one {
  flex-basis: 5rem;
}
```

```CSS
.box {
  flex-basis: 5;
  flex-grow: 1;
  width: 5rem;
  height: 5rem;
  background: gold;
  margin: 1rem;
}

.box-one {
  flex-grow: 0;
}
```

```CSS
.box {
  flex-basis: 15rem;
  flex-shrink: 1;
  width: 5rem;
  height: 5rem;
  background: gold;
  margin: 1rem;
}

.box-one {
  flex-shrink: 0;
}
```

```CSS
.box {
  /* flex-basis: 15rem;
  flex-shrink: 1;
  flex-grow: 1; */
  flex: 1 1 15rem;
  width: 5rem;
  height: 5rem;
  background: gold;
  margin: 1rem;
}
```

### Grid

- **FLEXBOX**: To lay out elements in a row or a column
- **GRID**: To lay out elements in **both** rows and columns

**DEFINEING A GRID**

- display: grid
- grid-template-rows
- grid-template-columns

```CSS
.container {
  display: grid;
  /* grid-template-rows: repeat(3, 100px);
  grid-template-columns: repeat(2, 100px); */
  grid-template: repeat(3, 100px) / repeat(2, 100px);
  border: 3px solid lightgray;
}
```

```HTML
  <body>
    <div class="container">
      <div class="box">A</div>
      <div class="box">B</div>
      <div class="box">C</div>
      <div class="box">D</div>
    </div>
```

```CSS
.container {
  display: grid;
  grid-template: repeat(3, 100px) / repeat(2, 100px);
  border: 3px solid lightgray;
}

.box {
  width: 5rem;
  height: 5rem;
  background: gold;
}
```

**ALIGNING ITEMS**

- justify-items (along the horizontal axis)
- align-items (along the vertical axis)

```CSS
.container {
  display: grid;
  grid-template: repeat(3, 100px) / repeat(2, 100px);
  border: 3px solid lightgray;
  justify-items: center;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
```

Default value of "justify-items" and "align-items" - stretch

```CSS
.container {
  display: grid;
  grid-template: repeat(3, 100px) / repeat(2, 100px);
  border: 3px solid lightgray;
  justify-items: stretch;
  align-items: stretch;
  height: 100vh;
}

.box {
  /* width: 5rem; */
  /* height: 5rem; */
  background: gold;
}
```

A fraction of the available space

```CSS
.container {
  display: grid;
  grid-template: repeat(3, 100px) / 100px 30fr 70fr;
  border: 3px solid lightgray;
  justify-items: stretch;
  align-items: stretch;
  height: 100vh;
}
```

Adding GAPs between rows and columns

- row-gap
- column-gap
- gap

```CSS
.container {
  display: grid;
  grid-template: 100px auto 100px / 30fr 70fr;
  row-gap: 10px;
  column-gap: 10px;
  /* gap: 10px, 20px; */
  border: 3px solid lightgray;
  justify-items: stretch;
  align-items: stretch;
  height: 100vh;
}
```

#### Placing Items

- grid-row
- grid-column
- grid-area

```CSS
.box-one {
  /* grid-column: 2; Move to line 2*/
  /* grid-column: 1 / 3; Occupy from line 1 to line 3*/
  /* grid-column: 1 / -1; -1 means the last item */
  grid-column: 1 / span 2;
  /* grid-row: 2; */

  /* start / end */
  /* row / comlumn */
  /* Too tricky, not use it! */
  grid-area: 1 / 1 / 1 / 3;
}
```

**PLACING ITEMS IN NAMED AERAS**

- grid-template-areas
- grid-area

```HTML
    <div class="container">
      <div class="box box-one">A</div>
      <div class="box">B</div>
      <div class="box">C</div>
      <div class="box box-four">D</div>
    </div>
```

```CSS
.container {
  display: grid;
  grid-template: 100px auto 100px / 30fr 70fr;
  row-gap: 10px;
  column-gap: 10px;
  grid-template-areas:
    "header header"
    "sidebar main"
    ".      footer";
  border: 3px solid lightgray;
  justify-items: stretch;
  align-items: stretch;
  height: 100vh;
}

.box {
  /* width: 5rem; */
  /* height: 5rem; */
  background: gold;
}

.box-one {
  /* grid-column: 1 / span 2; */
  grid-area: header;
}

.box-four {
  grid-area: footer;
}
```

### Hiding Elements

```HTML
    <p class="first">First</p>
    <p>Second</p>
```

```CSS
.first {
  /* display: none; */
  visibility: hidden;
}
```

## Media Queries

To provide different styles for different devices depending on their features.

**RESPONSIVE DESIGN**

- Desktop first
- Mobile first (Recommended)

https://ricostacruz.com/til/css-media-query-breakpoints

```HTML
    <div class="container">
      <div class="box">
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut
          accusantium soluta sit quia minus reiciendis iusto, consequatur quam
          numquam, in error tempore magnam tempora asperiores quod! Sed deleniti
          voluptates quas.
        </p>
      </div>
      <div class="box">
        <p>
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Mollitia
          accusamus, quos numquam nobis voluptate omnis sapiente doloribus
          architecto id, quidem odit officiis iste illum repellendus nulla
          praesentium! Alias, magni maiores?
        </p>
      </div>
    </div>
```

```CSS
.container {
  display: flex;
  flex-direction: column;
}

.box {
  background: gold;
  padding: 1rem;
}

.box:nth-of-type(2) {
  background: dodgerblue;
}

@media screen and (min-width: 600px) {
  .container {
    flex-direction: row;
  }
}

@media screen and (max-width: 900px) {
  .container {
    flex-direction: row;
  }
  .box {
    background: white;
  }
}
```

# Typography

- Styling fonts
- Embedded custom fonts
- Usin font services
- Using font services
- Best practices for text size & spacing
- Formatting text

## Styling Fonts

### font-family

- Serif

  - Professional and serious
  - New Times Roman
  - Georgia

- Sans-serif

  - Avenir
  - Arial
  - Futura
  - Helvetica
  - Roboto

- Monospace
  - Ideal to display codes
  - Consolas
  - Courier
  - Ubuntu

```HTML
    <h1>Heading</h1>
  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Enim officiis et
    suscipit. Optio, hic tempora facere esse ab minus repellat mollitia! Error
    distinctio fugit cumque hic voluptas sit, voluptates saepe!
  </p>
  <!-- The default hyperlink is Serif -->
  <a href="#">Link</a>
```

```CSS
body {
  margin: 10px;
  font-family: Arial, Helvetica, sans-serif;
}

h1 {
  font-family: Georgia, "Times New Roman", Times, serif;
}

p {
  font-weight: normal;
  font-style: italic;
  font-size: 1rem;
  color: #333;
}
```

## Embedded Fonts

**WHERE TO FIND FONTS**

- fontsquirrel.com
- fonts.com
- myfonts.com

**FONT FORMATS**

- TTF
- OTF
- EOT
- **WOFF** | More compressed
- **WOFF 2.0** |

Use the [GENERATER] in fontsquirrel.com to convert the ttf to woff/woff2.
Check the woff/woff2 feature in caniuse.com.

```CSS
@font-face {
  font-family: "opensans";
  src: url("fonts/open-sans/opensans-regular-webfont.woff2") format("woff2"),
    url("fonts/open-sans/opensans-regular-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: "opensans";
  src: url("fonts/open-sans/opensans-bold-webfont.woff2") format("woff2"),
    url("fonts/open-sans/opensans-bold-webfont.woff") format("woff");
  font-weight: bold;
  font-style: normal;
}

body {
  margin: 10px;
  font-family: "opensans", Arial, Helvetica, sans-serif;
}
```

## Flash of Unstyled Text

```CSS
font-display: optional;
```

The browser will download the font and store it in cache. If it is not in the cache -> swap.

Customer setting in the [GENERATER] of fontsquirrel.com to reduce the size as smaller.

## Font Services

- Google Web Fonts (fonts.google.com)
- Adobe Fonts (fonts.adobe.com)
- fonts.com
- fontdeck.com

**Query String Parameters** after the ? in the URL
"https://fonts.googleapis.com/css2?family=Open+Sans&family=Roboto:wght@400;700&display=swap"

- Parameter Name (family) = Parameter Value (string before the second &)
- "+" because URL doesn't have [empty space]
- "wght@" telling google using open-sans in the particular weights
- Remove the 700 of wght@400;700 due to no needs to use bold weight.
- Useing extra weight -> wght@400;700;600
- Using "&" to separte multipe parameters
- "&display=optional"

```HTML
    <title>Document</title>
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link
      href="https://fonts.googleapis.com/css2?family=Open+Sans&family=Roboto:wght@400;700&display=swap"
      rel="stylesheet"
    />
    <link rel="stylesheet" href="css/normalize.css" />
    <link rel="stylesheet" href="css/styles.css" />
```

```CSS
/* We don't need this any more once connected to fonts.google.com */
/* @font-face {
  font-family: "opensans";
  src: url("fonts/open-sans/opensans-regular-webfont.woff2") format("woff2"),
    url("fonts/open-sans/opensans-regular-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
  font-display: optional;
}

@font-face {
  font-family: "opensans";
  src: url("fonts/open-sans/opensans-bold-webfont.woff2") format("woff2"),
    url("fonts/open-sans/opensans-bold-webfont.woff") format("woff");
  font-weight: bold;
  font-style: normal;
  font-display: optional;
} */

body {
  margin: 10px;
  font-family: "Open Sans", Arial, Helvetica, sans-serif;
}

h1 {
  /* font-family: Georgia, "Times New Roman", Times, serif; */
  font-family: "Roboto", sans-serif;
}

p {
  font-weight: normal;
  font-style: italic;
  font-size: 1rem;
  color: #333;
}
```

## Sytem Font Stack

To tell the browser using the default fonts of the operating system of the user computer.

- Pros:

  - Can boost performance
  - No flash of unstyled text (FOUT)
  - Native look
  - Overall: better experience

- Cons:

  - Default fonts vary
    - macOS(Recent) -> San Francisco
    - macOS -> Helvetica Neue
    - Windows -> Segoe UI
    - Android -> Roboto

```CSS
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
```

## Sizing Fonts

Forget pixels setting because pixeles are not consistent across devices.

**RETINA DISPLAY TECHNOLOGY**
Apple devices such as iMac, iPhone or iPad allow pixels to be smaller => Everything looks very sharp on the screen.

**RELATIVE**

- % | relative to the size of the container
- vw |
  | relative to the viewpoint
- vh |
- em |
  | relative to the font size
- rem |

```CSS
html {
  /* Default is 16 px*/
  /* font-size: 16px; */
  /* 62.5% of 16px = 10px */
  font-size: 62.5%;
}

body {
  margin: 10px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-size: 1rem;
  /* 1 x font size of the root element -> font size set in the browser or the font-size defined in html {};*/
}

h1 {
  font-family: Georgia, "Times New Roman", Times, serif;
  /* font-family: "Roboto", sans-serif; */
  font-size: 2rem;
}

p {
  /* font-family: "Open Sans", Arial, Helvetica, sans-serif; */
  font-weight: normal;
  font-style: italic;
  font-size: 1rem;
  color: #333;
}

@media screen and (mid-width: 400px) {
  html {
    font-size: 150%;
  }
}
```

Check **_type-scale.com_**

```HTML
    <h1>Heading 1</h1>
    <h2>Heading 2</h2>
```

```CSS
h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: Georgia, "Times New Roman", Times, serif;
}

h1 {
  /* Got 4.209rem from type-scale.com*/
  font-size: 4.209rem;
}

h2 {
  /* Got 157rem from type-scale.com*/
  font-size: 3.157rem;
}
```

## Vertical Spacing

- margin
- line-height

**Law of Proximity**
Objects that are closer are perceived to be related.

```CSS
h1 {
  margin: 3rem 0 1rem;
}
```

```CSS
body {
  margin: 10px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-size: 1rem;
  /* line-height as always 1.5 times of font-size */
  line-height: 1.5;
}
```

## Horizontal Spacing

- letter-spacing -> using pixels
- word-spacing -> using pixcels
- width -> 50ch

**IDEAL LINE LENGTH**
Should be between 50 - 70 characters.

## Formatting Text

- text-align
- text-indent
- text-decoration
- text-transform
- white-space
- column-\*
- direction

```CSS
p {
  /* i 1 */
  width: 50ch;
  white-space: nowrap;
  border: 3px solid gold;
  overflow: hidden;
  /* Get ... at the end */
  text-overflow: ellipsis;
}
```

```CSS
p {
  width: 50ch;
  column-count: 2;
  column-gap: 1rem;
  column-rule: 3px dotted #999;
}
```

# Images

- Images types and formats
- Background images
- CSS sprites
- Data URLs
- Clipping images
- Applying filters
- Supporting high-density screens
- Resolution switching
- Using modern image formats (WebP)
- Art direction
- Scalable Vector Graphics (SVG)
- Icon fonts

## Images Types and Formats

- **RASTER**
  - Come from cameras/scanners
  - Formats: JPG, PNG, GIF, etc
    - JPEG: { Colors: 16M, Transparency: false, Animation: false}
    - GIF: { Colors: 256, Transparency: true, Animation: true}
    - PNG: { Colors: 16M, Transparency: true, Animation: true}
    - **WebP**: { Colors: 16M, Transparency: true, Animation: true}
  - More pixels = large file size
  - (Small size) Look blurry if scaled up
- **VECTOR**

  - Create in software (Adobe Illustrator)
  - Format: SVG
  - Scalable Vector Graphics
  - Look sharp at any size

## Content Images

Empty string as alt for some decorative images, to avoid reading the path of image.

```HTML
<img src="images/line.jpg" alt="">
```

```CSS
.coffee {
  width: 100vw;
}
```

Might see too much details on the blur images if setting 100vw. SVG doesn't have this problem.

## Background Images

```CSS
body {
  background: url(../images/bigship-bg.jpg);
  background-repeat: no-repeat;
  /* background-position: -100px 100px; */
  background-attachment: fixed;
  background-size: cover;
  height: 300vh;
}
```

## CSS Sprites

https://www.flaticon.com/

http://cssspritestool.com/

Search "css sprites generator" in google

**PROBLEMS**

- First size can get too large
- Spites are not flexible

## Data URLs

Formerly: Data URLs
Another optimization technique to reduce HTTP requests.

https://www.cssportal.com/image-to-data/

**PROBLEMS**

- Size of embedded code > size of the resource
- Increase complexity
- Slow on mobile

## Clipping

Search "css clip generator" in google.

```HTML
<img class="coffee" src="/images/coffee.jpg" alt="" />
```

Copied from the generator

```CSS
.coffee {
  clip-path: polygon(
    0% 20%,
    60% 20%,
    60% 0%,
    100% 50%,
    60% 100%,
    60% 80%,
    0% 80%
  );
}
```

## Filters

- grayscale
- blur
- constrast
- brightness
- saturate

```CSS
.coffee {
  filter: grayscale(70%) blur(3px);
}
```

**PSEUDO-CLASS SELECTORS**
To select an element in a particular class (state)

- :hover
- :active
- :visited

Search "css filter functions" in google

## Supporting High-density Screens

**TERMS**

- Physical resolution:The actual number pixels of a device => iPhone4 960 x 640
- Logical resolution: Basically how they behave => iPhone 480 X 320
  CSS is always based on a logical resolution.

- Device Pixel Ration(DPR): Physical / Logical => iPhone 2
- High Density: DPR > 1

```HTML
    <img
      class="coffee"
      src="/images/coffee.jpg"
      alt="A cup of coffee"
      srcset="
        images/coffee.jpg    1x,
        images/coffee@2x.jpg 2x,
        images/coffee@3x.jpg 3x
      "
    />
```

## Resolution Switching

**RETINA DISPLAYS**

- iPhone 8 776 x 375
- iPad Pro 11" 1024 x 768
- MacBook Pro 15" 1440 x 900

https://responsivebreakpoints.com/

```CSS
    <img
      class="vegetable"
      src="/images/vegetable.jpg"
      alt="A bunch of vegetable"
      srcset="
        images/vegetable.jpg     400w,
        images/vegetable@2x.jpg  800w,
        images/vegetable@3x.jpg 1200w
      "
      sizes="
      (max-width:500px) 100vw,
      (max-width:700px) 50vw,
      33vw
        "
    />
```

## Using Morden Image Formats

- Photoshop (webPshop plug-in)
- Sketch
- Online tools (cloudconvert.com/jpg-tp-webp)
- Command-line tools

```HTML
    <picture>
      <source type="image/webp" srcset="images/vegetable.webp" />
      <source type="image/jpg" srcset="images/vegetable.jpg" />
      <img src="images/vegetable.jpg" alt="A buch of vegetable" />
    </picture>
```

## Art Direction

```HTML
    <picture>
      <!-- Assumed 500px as mobile -->
      <source media="(max-width: 500px)" src="images/vegetable.jpg" />
      <source media="(min-width: 501px)" src="images/vegetable@2x.jpg" />
      <img src="/images/vegetable.jpg" alt="A bunch of vegetable" />
    </picture>
```

## Scalable Vector Graphics

- **VECTOR**

  - Create in software (Adobe Illustrator)
  - Format: SVG
  - Scalable Vector Graphics
  - Look sharp at any size

  https://www.svgbackgrounds.com/

## Icon Fonts

- Font Awesome https://fontawesome.com/
- Ionicons
- Material Design Icons

```HTML
    <span class="icon">
    <i class="fas fa-bell fa-2x"></i>
  </span>
```

```CSS
.icon {
font-size: 2rem;
color: dodgerblue;
}
```

# Forms

- Build forms
- Style forms
- Text fields
- Data lists
- Drop-down lists
- Check boxes
- Radio buttons
- Sliders
- File inputs
- Hidden fields
- Data validation
- Submitting forms

## Creating a Basic Form

```HTML
  <body>
    <form>
      <div class="form-group">
        <label for="name">Name</label>
        <input type="text" id="name" />
      </div>
      <div class="form-group">
        <label for="email">email</label>
        <input type="email" id="email" />
      </div>
      <button type="submit">Register</button>
      <button type="reset">Clear</button>
    </form>
  </body>
```

## Styling Form

```CSS
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  line-height: 1.5;
  padding: 1rem;
}

label {
  display: block;
}

input[type="text"],
input[type="email"] {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 0.5rem 0.7rem;
  transition: border-color 0.15s, box-shadow 0.15s;
}

input[type="text"]:focus,
input[type="email"]:focus {
  border-color: #7db0fb;
  outline: 0;
  box-shadow: 0 0 0 4px rgba(24, 177, 255, 0.25);
}

button {
  background: #0d6efd;
  color: #fff;
  border: 0;
  padding: 0.5rem 0.7rem;
  border-radius: 5px;
  outline: 0;
}

.form-group {
  margin-bottom: 1rem;
}
```

## CSS Framework

- Bootstrap
- Foundation
- Semantic UI
- UI Kit
- Materialize
- Milligram

### Bootstrap

getbootstrap.com

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="css/normalize.css" />
    <link rel="stylesheet" href="css/styles.css" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-wEmeIV1mKuiNpC+IOBjI7aAzPcEZeedi5yW5f2yOq55WWLwNGmvvx4Um1vskeMj0"
      crossorigin="anonymous"
    />
    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-p34f1UUtsS3wqzfto5wAAmdvj+osOnFyQFpp4Ua3gs/ZVWx6oOypYoCJhGGScy+8"
      crossorigin="anonymous"
    ></script>
    <script
      src="https://kit.fontawesome.com/09636f7394.js"
      crossorigin="anonymous"
    ></script>
  </head>
  <body>
    <form class="w-50">
      <div class="mb-3">
        <label class="form-label" for="name">Name</label>
        <input class="form-control" type="text" id="name" />
      </div>
      <div class="mb-3">
        <label class="form-label" for="email">Email</label>
        <input class="form-control" type="email" id="email" />
      </div>
      <button class="btn btn-primary" type="submit">Register</button>
      <button class="btn btn-secondary" type="reset">Clear</button>
    </form>
  </body>
</html>
```

### Milligram

http://milligram.io/

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="css/normalize.css" />
    <link rel="stylesheet" href="css/styles.css" />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/milligram/1.4.1/milligram.css"
    />
  </head>
  <body>
    <form>
      <div>
        <label for="name">Name</label>
        <input type="text" id="name" />
      </div>
      <div>
        <label for="email">Email</label>
        <input type="email" id="email" />
      </div>
      <button type="submit">Register</button>
      <button type="reset">Clear</button>
    </form>
  </body>
</html>
```

## Text Fields

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input

```HTML
    <form>
      <input type="email" placeholder="Email" value="lawjune@163.com" />
      <textarea name="" id="" cols="30" rows="10">Commemt...</textarea>
    </form>
```

```CSS
form {
  width: 50%;
  padding: 2rem;
}

textarea {
  resize: none;
}
```

## Data Lists

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist

```HTML
    <form>
      <input type="text" list="countries" autocomplete="off" />
      <datalist id="countries">
        <option data-value="1">Australia</option>
        <option>Canada</option>
        <option>India</option>
        <option>United States</option>
      </datalist>
    </form>
```

## Drop-down Lists

```HTML
    <form>
      <select>
        <optgroup label="Front-end Courses">
          <option value="1" selected>HTML</option>
          <option value="2">CSS</option>
          <option value="3">JavaScript</option>
        </optgroup>
        <optgroup label="Back-end Courses">
          <option value="1" selected>Node.js</option>
          <option value="2">ASP.NET</option>
          <option value="3">Django</option>
        </optgroup>
      </select>
    </form>
```

## Check Boxes

```HTML
    <form>
      <div>
        <input type="checkbox" id="front-end" disabled />
        <label class="label-inline" for="front-end">Front-end</label>
      </div>
      <div>
        <input type="checkbox" id="back-end" checked />
        <label class="label-inline" for="front-end">Back-end</label>
      </div>
    </form>
```

## Radio Buttons

```HTML
    <form>
      <div>
        <input type="radio" name="membership" id="silver" checked />
        <label for="silver" class="label-inline">Silver</label>
      </div>
      <div>
        <input type="radio" name="membership" id="gold" disabled />
        <label for="gold" class="label-inline">Gold</label>
      </div>
    </form>
```

## Sliders

```HTML
    <form>
      <input type="range" min="0" , max="100" , value="90" />
    </form>
```

## File Inputs

```HTML
    <form>
      <input type="file" multiple />
      <input type="file" accept=".jpg, .png" />
      <input type="file" accept="image/*" />
    </form>
```

## Grouping Related Fields

```HTML
    <form>
      <fieldset>
        <legend>Billing Address</legend>
        <input type="text" /><input type="text" /><input type="text" />
        <legend>Payment</legend>
        <input type="text" /><input type="text" /><input type="text" />
      </fieldset>
    </form>
```

## Hidden Fields

```HTML
    <form>
      <input type="hidden" name="course-id" , value="1234" />
    </form>
```

## Data Validation

- Required fields
- Emails
- Numbers
- Dates

```HTML
    <form>
      <div>
        <input type="text" required minlength="3" maxlength="10" />
        <button type="submit">Submit</button>
      </div>
      <div>
        <input type="email" required />
        <button type="submit">Submit</button>
      </div>
      <div>
        <input type="numbers" required min="0" max="100" />
        <button type="submit">Submit</button>
      </div>
    </form>
```

## Submitting the Form

http://formspree.io/

```HTML
    <form action="https://formspree.io/f/xvodkodo" method="POST">
      <input type="text" placeholder="Name" name="name" />
      <input type="text" placeholder="Email" name="email" />
      <!-- <input type="submit" value="Submit" /> -->
      <button type="submit">
        <!-- <i class="fas fas-alert"></i> -->
        Submit
      </button>
    </form>
```

# Transformatons/Transitions/Animations

## 2D Transformations

- rotate()
- scale()
- skew()
- translate()

```HTML
    <div class="box">
      Lorem ipsum, dolor sit amet consectetur adipisicing elit.
    </div>
```

```CSS
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.box {
  width: 100px;
  height: 100px;
  background: gold;
}

.box:hover {
  /* transform: rotate(15deg); */
  /* transform: scale(1.5); */
  /* transform: skew(15deg); */
  /* position: absolute; */
  /* transform: translate(10px, 10px); */
  transform: rotate(15deg) translateX(50px);
}
```

## 3D Transformations

```HTML
    <div class="container">
      <div class="box">
        Lorem ipsum, dolor sit amet consectetur adipisicing elit.
      </div>
      <div class="box box-special">
        Lorem ipsum, dolor sit amet consectetur adipisicing elit.
      </div>
    </div>
```

```CSS
.container {
  /* Shared the same perspective */
  perspective: 200px;
}

.container:hover .box {
  /* transform: perspective(200px) translateZ(50px); */
  /* transform: perspective(200px) rotateY(45deg); */
  transform: rotateY(45deg);
  transform-origin: 0 50%;
}

.container:hover .box-special {
  transform: rotateX(45deg);
}
```

## Transitions

https://cubic-bezier.com/#.17,.67,.83,.67

```CSS
.box {
  width: 100px;
  height: 100px;
  background: gold;
  /* transition: transform 0.5s linear 1s; */
  transition: transform 0.5s background 0.5s;
}

.box:hover {
  transform: rotate(45deg);
  background: dodgerblue;
}
```

## Animations

```CSS
@keyframes pop {
  0% {
    transform: scale(1);
  }

  25% {
    transform: scale(1.3);
  }

  50% {
    transform: rotate(45deg);
    background: tomato;
  }

  100% {
    transform: rotate(0);
    /* background: tomato; */
  }
}

.box {
  width: 100px;
  height: 100px;
  background: gold;
  /* animation-name: pop;
  animation-duration: 4s;
  animation-delay: 1s;
  animation-iteration-count: infinite;
  animation-timing-function: ease-out;
  animation-direction: alternate;
  animation-fill-mode: both; */
  animation: pop 4s ease-out 1s infinite alternate both;
}
```

## Reusable Animations

```HTML
    <div class="box animation-pop">
      Lorem ipsum, dolor sit amet consectetur adipisicing elit.
    </div>
```

```CSS
.box {
  width: 100px;
  height: 100px;
  background: gold;
}

.animation-pop {
  animation-name: pop;
  animation-duration: 4s;
  animation-delay: 1s;
  animation-iteration-count: infinite;
  animation-timing-function: ease-out;
  animation-direction: alternate;
}
```

https://animate.style/

# Writing Clean and Maintainable CSS

- CSS best practices
- CSS variables
- Object-oriented CSS
- BEM

## CSS Best Practices

- Follow a naming convention

  **kebab Case**

  ```CSS
  .nav-bar {}
  ```

  **Camel Case**

  ```CSS
  .navBar{}
  ```

- Create logical sections in your stylesheet

  ```CSS
  /* Basic styles */
  * {
    box-sizing: border-box;
  }

  html {
  }

  /* Typography */
  h1,
  h2,
  h3 {
  }

  /* Forms */

  /* Navigation Bar */
  ```

- Avoid over-specific selectors

  ```HTML
      <div class="nav">
        <ul class="items">
          <li>Link 1</li>
          <li>Link 2</li>
          <li>Link 3</li>
        </ul>
      </div>
  ```

  Over-specific example:

  ```CSS
  div.nav > ul.items > li {}
  ```

  Reduce the specifity

  ```HTML
      <div class="nav">
        <ul class="items">
          <li class="nav-item">Link 1</li>
          <li class="nav-item">Link 2</li>
          <li class="nav-item">Link 3</li>
        </ul>
      </div>
  ```

  ```CSS
  .item{}
  .nav-item {}
  ```

- Avoid !important
- Sort CSS properties (Use VS Code sorting command)
- Take advantage of style inheritance
- Extract repetitive patterns
- Avoid repetitive values (Keep it **DRY: Don't Repeat Yourself**)

## CSS Variable

```HTML
    <div class="one"></div>
    <div class="two"></div>
```

```CSS
:root {
  --color-primary: #ffdd36;
  --border-size: 2px;
  --border-radius: 10px;
}

.one {
  background: var(--color-primary);
}

.two {
  background: var(--color-primary);
}
```

## Object-oriented CSS

- Separate container and content

  ```HTML
      <header class="hero"><button class="btn">Sign Up</button></header>
      <aside class="aside-bar"><button class="btn">Contact</button></aside>
  ```

  ```CSS
  .btn {
    background: gold;
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }
  ```

- Separate struct and skin

  ```HTML
      <header class="hero">
        <button class="btn btn-primary">Sign Up</button>
      </header>
      <aside class="aside-bar">
        <button class="btn btn-secondary">Contact</button>
      </aside>
  ```

  ```CSS
  .btn {
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }

  .btn-primary {
    background: gold;
  }

  .btn-secondary {
    background: dodgerblue;
  }
  ```

## BEM (Block Element Modifier)

```CSS
    <div class="card card--popular">
      <header class="card__header">
        <span class="card__price"></span>
      </header>
      <div class="card__body">
        <button class="btn"></button>
      </div>
    </div>
```
