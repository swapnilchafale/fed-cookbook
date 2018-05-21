# Amdocs Frontend Cookbook

## Table of Contents

1. [Introduction](#introduction)
    - [Installation](#installation)
    - [Compile](#compile-project)
1. [Folder Structure](#folder-structure)
    - [File Naming](#file-naming)
    - [Sass](#sass-folder)
    - [HTML](#html-folder)
    - [Digital Experience Style Base](#digital-experience-style-base)
1. [HTML](#html)
    - [New Page Template](#new-page-template)
1. [CSS](#css)
    - [Formatting](#formatting)
    - [Comments](#comments)
    - [BEM](#bem)
    - [ID Selectors](#id-selectors)
    - [JavaScript hooks](#javascript-hooks)
    - [Border](#border)
1. [Sass](#sass)
    - [Syntax](#syntax)
    - [Ordering](#ordering-of-property-declarations)
    - [Variables](#variables)
    - [Mixins](#mixins)
    - [Extend directive](#extend-directive)
    - [Nested selectors](#nested-selectors)
1. [Grid System](#grid-system)
    - [Bootstrap Grid](#bootstrap-grid)
1. [Responsive](#responsive)
    - [Mobile First](#mobile-first)
    - [Break Points](#break-points)
    - [Ordering](#media-queries-ordering)

## Introduction

Welcome to Amdocs front end cook book.

### Installation

1. Clone git
2. Run "npm install" from "digital-style-l9" folder to install project dependencies

### Compile Project

build - build dist folder\
build:watch - build dist folder and watch for changes

Usage
```sh
npm run build:watch
```

**[⬆ back to top](#table-of-contents)**

## Folder Structure

### File Naming

* Use Dashes
* Don't use camelCase or PascalCase

**Bad:**

```
createCustomer.html
_CreateCustomer.scss
```

**Good:**

```
create-customer.html
_create-customer.scss
```

### Sass Folder

**base** folder is part of [Digital Experience Style Base](#digital-experience-style-base) - **Do not edit files in this folder**\
Only edit files on **self service** folder:

* components - components styles
* elements - elements styles
* mixins - mixins
* utils - utility styles
* variables - sass variables
* widgets - page specific styles (**consider renaming to pages instead**)

**inclusion files (located inside self service root):**\
\_components.scss, \_elements.scss, \_mixins.scss, \_utils.scss, \_variables.scss, \_widgets.scss

### HTML Folder

* pages - complete pages including layout and built from components and elements (TBD)
* components - complex components, such as: cart, forms, etc.
* elements - small reusable components, such: buttons, checkboxes, radio buttons, switch, etc.

### Digital Experience Style Base

A library created by Amdocs core team which includes a set of ready-to-use mixins and html components.

**DO NOT EDIT THIS FOLDER !!**

**[⬆ back to top](#table-of-contents)**

## HTML

### New Page Template

* All pages need to include ```.ds-frame``` on the root element.
* Directly bellow ```.ds-frame``` we add a ```.ds-frame-content```
* Your custom page code goes inside ```.ds-frame-content``` 

**Page Template:**

```html
<body>
  
    <section class="ds-frame">
        <!-- PLACEHOLDER FOR THE HEADER -->
        
        <div class="ds-frame-content">
        </div>

        <!-- PLACEHOLDER FOR THE FOOTER -->
    </section>
</body>
```

**Example:**

```html
<body>
  <section class="ds-frame">
    <!-- PLACEHOLDER FOR THE HEADER -->
    
    <!-- ds-frame-content -->
    <div class="ds-frame-content">
      
      <!-- ds-checkout -->
      <div class="ds-checkout">
        
        <!-- container -->
        <div class="container">

          <!-- row -->
          <div class="row">
            
            <!-- column -->
            <div class="col-md-8">
              <!-- custom component -->
              <div class="ds-checkout-personal-info">
                ...
              </div>
              <!-- /custom component -->
            </div>
            <!-- /column -->

            <!-- column -->
            <div class="col-md-4">
              <!-- custom component -->
              <div class="ds-cart-prices">
                ...
              </div>
              <!-- /custom component -->
            </div>
            <!-- /column -->

          </div>
          <!-- /row -->
        </div>
        <!-- /container -->
      </div>
      <!-- /ds-checkout -->

    </div>
    <!-- /ds-frame-content -->

    <!-- PLACEHOLDER FOR THE FOOTER -->
  </section>
</body>
```

**Class Behavior:**

```.ds-frame``` - Full width (100% of screen width)\
```.ds-frame-content``` - Limited width and screen centered (```margin: 0 auto;```)


**[⬆ back to top](#table-of-contents)**

## CSS

### Formatting

* Use hards tabs (4 spaces) for indentation
* Use [BEM methodology](#bem)
* Use dashes in class names
* Don't use camelCasing or PascalCasing in class names
* Do not use ID selectors
* Avoid attaching classes to elements in your stylesheet (i.e. don’t do div.header or h1.title)
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line
* Put blank lines between rule declarations

**Bad**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
    // ...
}
```

**Good**

```css
.avatar {
    border-radius: 50%;
    border: 2px solid white;
}

.one,
.selector,
.per-line {
    // ...
}
```

### Comments

* Prefer line comments (`//` in Sass-land) to block comments.
* Prefer comments on their own line. Avoid end-of-line comments.
* Write detailed comments for code that isn't self-documenting:
  - Uses of z-index
  - Compatibility or browser-specific hacks

### BEM

**BEM**, or “Block-Element-Modifier”, is a _naming convention_ for classes in HTML and CSS. It was originally developed by Yandex with large codebases and scalability in mind.

  * It helps create clear, strict relationships between CSS and HTML
  * It helps us create reusable, composable components
  * It allows for less nesting and lower specificity
  * It helps in building scalable stylesheets

**Links**

  * CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

**Example**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="listing-card listing-card--featured">

      <h1 class="listing-card__title">Adorable 2BR in the sunny Mission</h1>

      <div class="listing-card__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```sass
/* listing-card.scss */
.listing-card { 
    &--featured { }
    &__title { }
    &__content { }
}
```

  * `.listing-card` is the “block” and represents the higher-level component
  * `.listing-card__title` is an “element” and represents a descendant of `.listing-card` that helps compose the block as a whole.
  * `.listing-card--featured` is a “modifier” and represents a different state or variation on the `.listing-card` block.

### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

### Border

Use `0` instead of `none` to specify that a style has no border.

**Bad**

```css
.foo {
    border: none;
}
```

**Good**

```css
.foo {
      border: 0;
}
```

**[⬆ back to top](#table-of-contents)**

## Sass

### Syntax

* Use the `.scss` syntax, never the original `.sass` syntax
* Order your regular CSS and `@include` declarations logically (see below)

### Ordering of property declarations

1. Nested selectors

    Nested selectors, _if necessary_, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### Variables

Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$_my-variable`).

TODO: Extend on when to use variables.

### Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.

### Extend directive

`@extend` should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using `@extend`, and you can DRY up your stylesheets nicely with mixins.

### Nested selectors

**Do not nest selectors more than three levels deep!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

When selectors become this long, you're likely writing CSS that is:

* Strongly coupled to the HTML (fragile) *—OR—*
* Overly specific (powerful) *—OR—*
* Not reusable


Again: **never nest ID selectors!**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.

**[⬆ back to top](#table-of-contents)**

## Grid System

### Bootstrap Grid

Our grid system was forked from bootstrap 3 and uses the same classes for page layout.

* Rows must be placed within a ```.container``` (fixed-width) or ```.container-fluid``` (full-width) for proper alignment and padding.
* Use rows to create horizontal groups of columns.
* Content should be placed within columns, and only columns may be immediate children of rows.
* Predefined grid classes like ```.row``` and ```.col-xs-4``` are available for quickly making grid layouts. Sass mixins can also be used for more semantic layouts.
* Columns create gutters (gaps between column content) via padding. That padding is offset in rows for the first and last column via negative margin on ```.row```s.
* The negative margin is why the examples below are outdented. It's so that content within grid columns is lined up with non-grid content.
* Grid columns are created by specifying the number of twelve available columns you wish to span. For example, three equal columns would use three ```.col-xs-4```.
* If more than 12 columns are placed within a single row, each group of extra columns will, as one unit, wrap onto a new line.
* Grid classes apply to devices with screen widths greater than or equal to the breakpoint sizes, and override grid classes targeted at smaller devices. Therefore, e.g. applying any ```.col-md-*``` class to an element will not only affect its styling on medium devices but also on large devices if a ```.col-lg-*``` class is not present.

**Avaliable classes:**

- ```.container```
- ```.row```
- ```.col-xs-1```, ```.col-xs-2```, ```.col-xs-3```, ..., ```.col-xs-12```
- ```.col-sm-1```, ```.col-sm-2```, ```.col-sm-3```, ..., ```.col-sm-12```
- ```.col-md-1```, ```.col-md-2```, ```.col-md-3```, ..., ```.col-md-12```
- ```.col-lg-1```, ```.col-lg-2```, ```.col-lg-3```, ..., ```.col-lg-12```

**Example:**

```html
<div class="container">
    <section class="row">
        <article class="col-md-6 col-lg-3">...</article>
        <article class="col-md-6 col-lg-3">...</article>
        <article class="col-md-6 col-lg-3">...</article>
        <article class="col-md-6 col-lg-3">...</article>
    </section>
</div>
```

## Responsive

### Mobile First

A mobile-first approach to styling means that styles are applied first to mobile devices. Advanced styles and other overrides for larger screens are then added into the stylesheet via media queries.

```scss
// This applies from 0px to $screen-xs (480px)
body {
    background: red;
}
```

```scss
// This applies from $screen-xs (480px) onwards
@media (min-width: $screen-xs) {
    body {
        background: green;
    }
}
```

### Break Points

We use the following media queries to create the key breakpoints in our grid system.

@media only screen and (min-width: $screen-xs) { ... }\
@media only screen and (min-width: $screen-sm) { ... }\
@media only screen and (min-width: $screen-md) { ... }\
@media only screen and (min-width: $screen-lg) { ... }

### Media Queries Ordering

Use media queries at the end of your Sass file.

**Bad**
```scss
.item {
    padding: 26px;
    
    @media screen and (min-width: $screen-md) {
        padding: 10px;
    }
}
```

**Good**
```scss
.item {
    padding: 26px;
}

...

@media screen and (min-width: $screen-md) {
    .item {
        padding: 10px;
    }
}
```

**[⬆ back to top](#table-of-contents)**