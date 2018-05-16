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
    - [Grid](#grid)
    - [Page Structure](#page-structure)
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
1. [Responsive](#responsive)
    - [Mobile First](#mobile-first)
    - [Break Points](#break-points)
    - [Ordering](#media-queries-ordering)

## Introduction

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

...

### Sass Folder

...

### HTML Folder

...

### Digital Experience Style Base

...

**[⬆ back to top](#table-of-contents)**

## HTML

### Grid

### Page Structure

```html
<!doctype html>
<html>
<head>
</head>
<body>
    <section class="ds-frame">

        <div class="ds-frame-content">
            <!-- PLACEHOLDER FOR THE HEADER -->

            <!-- PLACEHOLDER FOR THE WIDGET -->
            <div class="ds-footer-new"></div>
        </div>

        <div class="ds-ctc-placeholder">
            <button class="ds-btn ds-btn--large">CTCPlaceholder</button>
        </div>

        <div class="ds-tobi">
            <div class="ds-tobi__wrapper">
                <div class="ds-tobi__media"></div>
            </div>
        </div>

        <!-- PLACEHOLDER FOR THE FOOTER -->
    </section>
</body>
</html>
```

(**Todo:** Update classes to match guidelines)

**[⬆ back to top](#table-of-contents)**

## CSS

### Formatting

* Use hards tabs (4 spaces) for indentation
* Use [BEM methodology](#bem)
* Prefer dashes over camelCasing in class names.
  * Underscores and PascalCasing are okay if you are using BEM (see OOCSS and BEM below).
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

We recommend a variant of BEM with PascalCased “blocks”, which works particularly well when combined with components (e.g. React). Underscores and dashes are still used for modifiers and children.

**Example**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```sass
/* ListingCard.scss */
.ListingCard { 
    &--featured { }
    &__title { }
    &__content { }
}
```

  * `.ListingCard` is the “block” and represents the higher-level component
  * `.ListingCard__title` is an “element” and represents a descendant of `.ListingCard` that helps compose the block as a whole.
  * `.ListingCard--featured` is a “modifier” and represents a different state or variation on the `.ListingCard` block.

### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

### JavaScript hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

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

1. Property declarations

    List all standard property declarations, anything that isn't an `@include` or a nested selector.

    ```scss
    .btn--green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. `@include` declarations

    Grouping `@include`s at the end makes it easier to read the entire selector.

    ```scss
    .btn--green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. Nested selectors

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