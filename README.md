# Responsive Design and Advanced CSS

(Thanks for [voting](https://strawpoll.com/sssys43a)!)

What we'll cover:

**First half**:

1. The need for mobile-first design
2. Media queries
3. CSS grid

**Second half**:

5. CSS Preprocessors (SASS, CSS preset env)
6. Flexbox responsive patterns (demos)

## Responsive Design Patterns

Most users expect a `block`-style, vertically-scrolling layout on mobile; **this is the default `display` style of elements**

![mobile-first layout](https://uploads.toptal.io/blog/image/125541/toptal-blog-image-1520235926914-8f4727131d99922cc281d325ca1ab19a.png)

### Mobile-first
Design for phone screen first (ie. `block` layout); then use media queries for other devices

Not a one-size-fits-all solution; **In the real world, we need to prioritize early prototyping with the customer to determine requirements**.  This is known as [**requirements elicitation**](https://en.wikipedia.org/wiki/Requirements_elicitation)

## Media Queries
Used to change appearance when the browser size changes

Also for applying CSS in specific cases:

* Device orientation
* Device light exposure
* Devices lacking support for newer CSS features
* Devices with specific pixel densities (retina, high-density pixels)

Syntax:

```css
@media screen and (max-width: 50em) {

}
```

### Media Queries vs. Mobile-specific Websites

Whenever you see `m.` subdomains on websites like `m.cnn.com`, etc.

Google penalizes you for this, so avoid it if you want SEO

### Media Queries in HTML
Using `<link href>`, we can use the `media` attribute:

```html
<link href="path/to/style.css" media="screen and (orientation: portrait)"/> <!-- Only loads this CSS file on mobile phones; performant! -->
```

Loads styles conditionally, reducing file load.  Increases performance.

### Units

[**Do not use `px` for your media queries**](https://zellwk.com/blog/media-query-units/)

No:

```css
@media screen and (max-width: 768px) {

}
```

Yes:

```css
@media screen and (max-width: 55em) {

}
```

Remember: __using `em`s allows your UI to adapt to user zoom preferences__.  Using `em` project-wide allows us to scale our sizes rapidly with CSS.

## CSS Grid vs. flexbox
Hot topic in the industry today

Go-to resource: **[grid by example design patterns](https://gridbyexample.com/patterns/)**

See [the MDN article](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Relationship_of_Grid_Layout)

Flexbox:

* Requires more code
* Limited to one single axis (horizontal or vertical)
* Powers more of the web
* Has more documentation
* Has unified support

Grid:

* Requires less code
* Greatly simplifies complex designs along the vertical axis
* Has unified support
* Has a steeper learning curve

Resources:

* [A complete guide to grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
* [Box alignment cheatsheet](https://rachelandrew.co.uk/css/cheatsheets/box-alignment)

**Bottom line**: use CSS grid when you encounter trouble with flexbox or when you can't change your markup (ex. `<dl>` with `<dt>` and `<dd>`s)

## CSS Preprocessors
SASS is the most popular.

### Nesting

```css
.foo .bar .baz {

}
```

Replaced with:

```scss
.foo {
	.bar {
		.baz {

		}
	}
}
```

### Variables

```scss
$backgroundColour: hotpink !default;

body {
	background-color: $backgroundColour;
}
```

### Colour Functions

### Mixins

### Conditionals

### Placeholders

### Partials & `@import`

### Configuration with NodeJS

## Closing Thoughts

* Avoid frameworks and keep it simple (#1 comment from previous cohorts)
* Only nest selectors up to two levels -- or [don't nest at all](https://csswizardry.com/2017/02/code-smells-in-css-revisited/)
* Consider turning mixins into utility classes; avoid `@extends`
* Minimize breakpoints (media queries); reduce them to 2 or 3 (or less)
* Leverage mentor support; don't hesitate to use CSS grid
* Write your CSS grid layout in a `@supports(display: grid)`

Amuse yourself, when possible, with [css humour](https://csshumor.com/)

### Accessibility Thoughts
* Avoid changing the order of your content with CSS
* Keep your links underlined, looking like links; links are not `<button>`s
* [Avoid `outline: none`](http://www.outlinenone.com/) on your focused form fields or `<a>` tags
* Use `em` or `rem` when possible, especially in media queries
* Load your desktop styles in a separate file.  Speed up mobile performance


### Other CSS Code Smells

* `!important`
* `@import`
* `*` selector (selecting all the things)
* Setting `width` or `height`; use `min-width` or `min-height` instead

#### Excessively Long Selectors

No:

```css
.foo .bar .baz {
	/* 3 levels deep: nono */
}
```

Better:

```css
.foo .baz {
	/* 2 levels deep; questionable */
}
```

Good:

```css
.baz {

}
```

Best:

*No CSS*