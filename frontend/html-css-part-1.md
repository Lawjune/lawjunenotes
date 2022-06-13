# Getting Started

moshified.com

# Web Development Fundamentals

- The languages & tools of web development
- Key concepts (e.g. URL, HTTP, DOM, etc)
- How websites work
- Inspect network traffic using DevTools
- Basic HTML& CSS
- Validating web pages

## Languages and Tools of Web Development

- (Markup Language) HTML - Hypertext Markup Language - Building blocks of a webpage
- (Styling Language) CSS - Cascading stylesheet - Styling webpages and make them beautiful
- (Programming Language) JavaScript - Adding functionality to web pages

## How the Web Works

URL - Uniform Resource Location
Resources:

- Web pages (HTML documents)
- Images
- Video files
- Fonts
- ...

Client (Browser) ----HTTP(s)---> (Web) Server

Request:

```HTTP
GET /index.html HTTP/1.1
Host: www.codewithmosh.com
Accept-Language: en-us
```

Response:

```HTTP
HTTP/1.1 200 OK
Date: 1 Jan 2021 09:00
Content-Type: text/html

<!DOCTYPE html>
<html>
...
</html>
```

Browser will create a DOM(Document Object Model) while receiving http response with html document.

## Inspecting HTTP Requests and Response

Chrome - DevTools

## HTML Basics Started

```HTML
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First WebPage</title>
</head>

<body>
    <img src="images/pic.png">
    <p>@jluo33</p>
    <P>I love to learn HTML!</P>
</body>

</html>
```

## CSS Basics Started

```HTML
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First WebPage</title>
    <style>
        img {
            width: 100px;
            border-radius: 50px;
            float: left;
            margin-right: 10px;
        }

        .username {
            font-weight: bold;
        }
    </style>
</head>

<body>
    <img src="images/pic.png">
    <p class="username">@jluo33</p>
    <P>I love to learn HTML!</P>
</body>

</html>
```

## Validate the Web Pages

https://validator.w3.org/

# HTML Basics

- Text
- Links
- Images
- Lists & tables
- Container element
- Structral elements

## The Head Sections

### Character Set

Computers don't understand characters like A, B, C and so on, they only understand numbers which are represented by binary format.

Using _character set_ can map the characters to numeric value.

**ASCII** American Standard Code for Information Interchange
**UTF-8**

### View Port

The visible area of a web page.

```HTML
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

These are essential of making web page beautiful on all of devices.

### Meta Elements used for Searching

```HTML
    <meta name="keywords" content="HTML, CSS" />
    <meta name="description" content="..." />
```

## Text

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My First WebPage</title>
    <!-- Change the defualt emphasize style -->
    <style>
      em {
        color: red;
        font-style: normal;
      }
    </style>
  </head>

  <body>
    <h1>Heading 1</h1>
    <p>Each page should have only <em>one</em> single <em>h1 element</em>,</p>
    <h2>Heading 2</h2>
    <h3>Heading 3</h3>
    <h4>Heading 4</h4>
    <h5>Heading 5</h5>
    <h6>Heading 6</h6>
    <p>I love to learn <em>HTML</em>!</p>
    <!-- <p>I love to learn <i>HTML</i>!</p> -->
    <p>I love to learn <strong>HTML</strong>!</p>
  </body>
</html>
```

## Entities

```HTML
<p>I love to learn &lt;HTML>!</p>
<p>I love to learn &lt;HTML&gt;! &copy;</p>
```

Search "html entities"

"lorem"

## Hyperlinks

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Index</title>
  </head>
  <body>
    <a href="company/about.html">About Me</a>
    <a href="images/pic.png" download>My Photoe</a>
    <a href="#section-css">CSS</a>
    <a href="https://google.com">google</a>
    <a href="https://google.com" target="_blank">google with a new tab</a>
    <a href="mailto:lawjune@163.com">Email me</a>

    <h2 id="section-html">HTML</h2>
    <p>Lorem</p>
    <h2 id="section-css">CSS</h2>
    <p>Lorem</p>
    <a href="#">Jump to Top</a>
  </body>
</html>
```

## Images

Free images website: **_unsplash.com_**

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      img {
        width: 200px;
        height: 200px;
        object-fit: cover;
      }
    </style>
  </head>
  <body>
    <img src="images/coffee.jpg" alt="A coffee mug on a table" />
  </body>
</html>
```

## Vidoe and Audio

**_sketch.com_**

**_pexels.com_**

Check the feature of browsers in **_caniuse.com_**

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      video {
        width: 400px;
      }
    </style>
  </head>
  <body>
    <video controls autoplay loop src="videos/ocean.mp4">
      Your browser doesn't support videos.
    </video>
    <audio src=""></audio>
  </body>
</html>
```

## Lists

ul>li\*3

```HTML
    <style>
      ul {
        list-style-type: none;
      }
    </style>

    <ul>
      <li>About me</li>
      <li>
        Courses
        <ul>
          <li>HTML&CSS</li>
          <li>JavaScript</li>
          <li>Git</li>
        </ul>
      </li>
      <li>Subscribe</li>
      <li>Contact me</li>
    </ul>
```

```HTML
    <ol>
      <li>Preheat the oven.</li>
      <li>Place the ingridents on the crust.</li>
      <li>Put the pizza in the oven for 20 minutes.</li>
    </ol>
```

```HTML
    <dl>
      <dt>Title</dt>
      <dd>The Ultimate HTML and CSS Course</dd>
      <dt>Learner</dt>
      <dd>Jun Luo</dd>
      <dt>Skills</dt>
      <dd>HTML</dd>
      <dd>CSS</dd>
      <dd>Responsive Design</dd>
      <dd>Search Engine Optimization</dd>
    </dl>
```

## Tables

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      table,
      td,
      th {
        border: 1px solid gray;
        border-collapse: collapse;
        padding: 5px;
      }
      /* td {
        border: 1px solid gray;
      } */
      tfoot {
        text-align: left;
      }
    </style>
  </head>
  <body>
    <table>
      <thead>
        <tr>
          <th colspan="2">Expenses</th>
        </tr>
        <tr>
          <th>Category</th>
          <th>Amount</th>
        </tr>
      </thead>

      <tbody>
        <tr>
          <td>Marketing</td>
          <td>$100</td>
        </tr>
        <tr>
          <td>Accounting</td>
          <td>$200</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <th>Total</th>
          <th>$300</th>
        </tr>
      </tfoot>
    </table>
  </body>
</html>
```

## Containers

### <div> - Block Level Element

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .product {
        background-color: greenyellow;
        width: 300px;
      }
    </style>
  </head>
  <body>
    <div class="product">
      <p>Lorem ipsum dolor sit amet.</p>
      <a href="#">Link</a>
    </div>

    <div class="product">
      <p>Lorem ipsum dolor sit amet.</p>
      <a href="#">Link</a>
    </div>
  </body>
</html>
```

### <span> - Inline Element

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .highlight {
        background-color: yellow;
      }
    </style>
  </head>
  <body>
    <p>
      <span class="highlight">Lorem</span>
      ipsum dolor sit amet consectetur adipisicing elit. Ea culpa dolorum
      aliquam quam eveniet, harum dolore error similique neque nostrum, ipsa,
      earum eum voluptate iste magnam iusto deleniti iure nam.
    </p>
  </body>
</html>
```

### Semantic Elements

- **GENERIC CONTAINERS**
  - <div>
  - <span>
- **SEMANTIC CONTAINERS**
  - <article>
  - <figure>
  - <mark>
  - <time>

```HTML
  <body>
    <article class="article">
      <h1>Heading</h1>
      <p>
        Publish <time datetime="2021-01-01 17:00">January 1 2021 05:00pm</time>
      </p>
      <p>
        <mark>Lorem</mark> ipsum dolor sit amet, consectetur adipisicing elit.
        Cum, exercitationem est ad, repellat officiis voluptas aperiam
        repellendus sapiente quod quaerat itaque alias laboriosam non, nobis
        obcaecati placeat quasi pariatur atque!
      </p>
      <figure>
        <img src="" alt="" />
        <figcaption>My coffe this morning</figcaption>
      </figure>
    </article>
  </body>
```

- An independent, self-contained content

  - Forum post
  - Comments
  - Reviews
  - Product cards

## Structuring a Web Page

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li></li>
          <li></li>
          <li></li>
        </ul>
      </nav>
    </header>
    <main>
      <section>
        <h2>Products</h2>
        <article></article>
        <article></article>
        <article></article>
        <article></article>
      </section>
      <section>
        <h2>Testimoial</h2>
        <article>
          <section></section>
          <section></section>
          <section></section>
        </article>
        <article></article>
      </section>
    </main>
    <aside></aside>
    <footer>
      <nav>
        <ul>
          <li></li>
          <li></li>
          <li></li>
        </ul>
      </nav>
    </footer>
  </body>
</html>
```

# CSS Basics

- Various ways to provide CSS
- Normalizing CSS
- Selectors
- Colors
- Gradients
- Borders
- Shadows

## Providing CSS

- Embedded stylesheets -> X voilates **Separation of Concerns**
- External stylesheets
- Inline styles

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="styles.css" />
    <!-- Used embedded stylesheet to override the linked setting -->
    <style>
      p {
        color: black;
      }
      #first {
        color: blue;
        font-weight: bold;
      }
    </style>
  </head>
  <body>
    <!-- Avoid inline style setting as much as possible! -->
    <p id="first">Lorem ipsum dolor sit amet.</p>
    <p>Lorem ipsum dolor sit amet.</p>
  </body>
</html>
```

## Normalize.css

```HTML
    <link rel="stylesheet" href="css/normalize.css" />
    <link rel="stylesheet" href="css/styles.css" />
```

css/styles.css

```CSS
body {
  margin: 10px;
}

p {
  color: orange;
}
```

## Basic Selectors

- Type
- ID
- Class
- Attribute

```HTML
    <section id="products">
      <article class="product"></article>
      <article class="product"></article>
      <article class="product"></article>
```

```CSS
#products {}

.prudcot {}
```

```HTML
<a href="https://google.com" , target="_blank">google</a>
```

```CSS
a[href*="google"] {
  color: yellow;
}
```

```CSS
a[href^="https"] {
  color: yellow;
}
```

```CSS
a[href^="https"][href$=".com"] {
  color: yellow;
}
```

_Multiple elements can have the same class, but one id can only be corresponding to one element._

## Relational Selectors

```HTML
    <section id="products">
      <p>Lorem ipsum dolor sit amet.</p>
    </section>
```

```CSS
#products p {
  color: orange;
}
```

```HTML
    <section id="products">
      <!-- Only the first line paragraph highlighted -->
      <p>Lorem ipsum dolor sit amet.</p>
      <article>
        <p>Lorem ipsum dolor sit amet.</p>
      </article>
    </section>
```

```CSS
#products > p {
  color: orange;
}
```

```HTML
    <section id="products">
      <p>Lorem ipsum dolor sit amet.</p>
      <article>
        <p>Lorem ipsum dolor sit amet.</p>
      </article>
    </section>
    <!-- Only the 3rd line paragraph outside the section highlighted -->
    <p>Lorem ipsum dolor sit amet.</p>
    <p>Lorem ipsum dolor sit amet.</p>
```

```CSS
#products + p {
  color: orange;
}
```

```HTML
    <section id="products">
      <p>Lorem ipsum dolor sit amet.</p>
      <article>
        <p>Lorem ipsum dolor sit amet.</p>
      </article>
    </section>
    <!-- The below line paragraph outside the section highlighted -->
    <p>Lorem ipsum dolor sit amet.</p>
    <p>Lorem ipsum dolor sit amet.</p>
```

```CSS
#products ~ p {
  color: orange;
}
```

**_Need to be aware of_**

- Cleaner markup
- Can be fragile
- Not as fast as basic selectors

## Pseudo-class Selectors

```HTML
  <body>
    <article>
      <!-- Effect on the first paragraph -->
      <p>Lorem ipsum dolor sit amet.</p>
      <p>Lorem ipsum dolor sit amet.</p>
    </article>
  </body>
```

_It's very fragile._

```CSS
article :first-child {
  font-size: 140%;
  font-style: italic;
}
```

```HTML
  <body>
    <article>
      <!-- Effect on the first h2 and paragraph both-->
      <h2>Heading</h2>
      <p>Lorem ipsum dolor sit amet.</p>
      <p>Lorem ipsum dolor sit amet.</p>
    </article>
  </body>
```

```CSS
article :first-of-type {
  font-size: 140%;
  font-style: italic;
}
```

Same effect on the last

```CSS
article :last-of-type {
  font-weight: bold;
}
```

```HTML
<!-- ul>li*5{Item $} -->
      <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
        <li>Item 4</li>
        <li>Item 5</li>
      </ul>
```

```CSS
ul li:nth-child(odd) {
  color: deeppink;
}
```

```HTML
<a href="https://someweirdwebsite.com">Link</a>
```

```CSS
a:visited a:link {
  color: dodgerblue;
}

a:hover a:focus {
  color: deeppink;
}
```

## Pseudo-element Selectors

```HTML
    <p>
      <span class="first-letter">L</span>orem ipsum dolor sit, amet consectetur
      adipisicing elit. Minima molestiae eaque, ex corporis neque quidem
      obcaecati beatae repudiandae a eveniet blanditiis, possimus quas natus
      quisquam dignissimos. Nisi illum blanditiis quidem!
    </p>
```

```CSS
.first-letter {
  font-size: 140%;
  font-weight: bold;
}
```

Same result as above!

```CSS
p::first-letter {
  font-size: 140%;
  font-weight: bold;
}
```

- **_PSEUDO-ELEMENTS_**

  - **To style part of an element**
  - Eg. First letter

- **_PSEUDO-CLASSES_**
  - **To style elements in a particular state**

```CSS
p::first-line {
  font-weight: bold;
}

::selection {
  background-color: pink;
}

p::before {
  content: "...";
  /* block : new line */
  display: block;
}

p::after {
  content: "...";
  /* block : new line */
  font-weight: bold;
  display: block;
}
```

## Selectors Specificity

```HTML
    <article>
      <h1 class="highlight">Heading</h1>
    </article>
```

```CSS
body {
  margin: 10px;
}

h1 {
  color: dodgerblue;
}

.highlight {
  color: deeppink;
}

#products {
  color: green;
}

/* Effective selector */
#products {
  color: brown;
}
```

**_ID selector_** #products
**_Class & attribute selectors_** .products

```CSS
/* Considered as bad practice! */
h1 {
  color: dodgerblue !important;
}

.highlight {
  color: deeppink;
}

#products {
  color: green;
}

/* elector Specificity: (1, 0, 0) */
#products {
  color: brown;
}
```

**_Selector Specificity: (1, 0, 0)_**
First 1: # of ID selectors
Second 0: # of class/attribute selectors
Third 0: # of element selectors

```CSS
/* elector Specificity: (1, 1, 0) */
.highlight#products {
  color: dodgerblue;
}

/* elector Specificity: (1, 0, 1) */
h1#products {
  color: dodgerblue;
}
```

## Inheritance

```HTML
<p>Lorem ipsum <strong>dolor</strong> sit amet.</p>
```

```CSS
p {
  color: dodgerblue;
  border: 1px solid black;
}

/* Not inheritant from p */
strong {
  color: initial;
  /* border needs to inherit explictly */
  border: inherit;
}
```

## Colors

**_Ways of represent colors_**

- Named colors
- RGB
- HSL
- Hexadecimal

Search "color picker" in google

```HTML
    <div class="box"></div>
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: black;
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: rgb(230, 205, 16);
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: rgba(230, 205, 16, 0.5);
  /* Use a to manage the transparency level */
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: #e6cd10;
  /* No transparency level setting */
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: hsl(hue, saturation, lightness);
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: hsla(53, 40%, 60%, 0.4);
}
```

## Gradients

```CSS
.box {
  width: 200px;
  height: 200px;
  background: linear-gradient(dodgerblue, yellow);
  background: linear-gradient(to bottom right, dodgerblue, yellow);
  background: linear-gradient(45deg, dodgerblue, yellow 90%);
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background: radial-gradient(circle, dodgerblue, yellow 90%);
  background: radial-gradient(circle at top left, dodgerblue, yellow 90%);
}
```

Search "gradient generator" in google.

## Borders

```CSS
.box {
  width: 200px;
  height: 200px;
  background: dodgerblue;
  border: 10px solid royalblue;
  border-top: 20px solid royalblue;
  border-width: 10px 20px 10px 20px;
  /* 10px 20px == 10px 20px */
  /* 10px == 10px 10px 10px 10px */

  border-radius: 50px;
  /* 100% -> circle */
  border-radius: 100%;
}
```

- solid
- dotted
- dashed

Search "css shapes" in google.

## Shadows

```HTML
  <body>
    <div class="box">
      <h1>Heading</h1>
    </div>
  </body>
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background: gold;
  /* box-shadow: 10px 10px 30px grey; */
  box-shadow: 0 0 30px grey;
}

h1 {
  color: white;
  text-shadow: 3px 3px 5px rgba(0, 0, 0, 0.2);
}
```
