---
title: Promos
summary: A promo is a snippet of content which links to a full piece of content elsewhere on the BBC site or app.
version: 0.1.0
published: false
accessibility: false
linkback: http://www.bbc.co.uk/gel/guidelines/promos
---

## Introduction

The **Promo** component is used to advertise BBC content. Principally it is a link to that content, but it can include a combination of supporting content to draw the reader's attention, such as media, data, and information about the content's author.

The full range of supporting **Promo** content is outlined on the [GEL Promo page](https://www.bbc.co.uk/gel/guidelines/promos).

## Recommended markup

**Promos** can appear individually or in groups. In either case, they should be marked up inside an `<aside>` (complementary landmark[^1]). This marks the **Promo(s)** out as being tangential; they break away from the host page's main content to suggest complementary reading or resources.

```html
<aside aria-labelledby="unique-promo-label">
  <span id="unique-promo-label" hidden>Related programmes</span>
  <!-- promo(s) here -->
</aside>
```

Note the labeling mechanism. Complementary landmarks are discoverable by screen reader users through browsing, or perusing aggregated landmark lists. The label identifies the specific purpose of the landmark. Suitable labels include _"Related"_, _"Read more"_, or _"More like this"_.

In this case, the label is removed from the DOM with `hidden` because a visual label has been deemed unnecessary. This does not suppress the labeling mechanism; screen readers still announce _"complementary, related programmes"_ or similar. Where appropriate, you can instead provide a visible label (by removing `hidden`). You can also use a heading, if you think it is beneficial for the promos to be considered part of the page's main structure and table of contents.

```html
<aside aria-labelledby="unique-promo-label">
  <h2 id="unique-promo-label">Related programmes</h2>
  <!-- promo(s) here -->
</aside>
```

You must choose a heading level that is appropriate for the context[^2]. For example, if the promos can be considered a child subsection of the page, use an `<h2>`. 

* Main heading (`<h1>`)
    * Subsection heading (`<h2>`)
    * Another subsection heading (`<h2>`)
    * Read more (`<h2>`) ← The Promo landmark

### Groups of promos

A group of promos should be marked up as a list. This enables structural and navigational cues in screen reader software[^3].

```html
<aside aria-labelledby="unique-promo-label">
  <span class="gef-sr" id="unique-promo-label">More like this</span>
  <ul class="gef-promos">
    <li class="gef-promo">...</li>
    <li class="gef-promo">...</li>
    <li class="gef-promo">...</li>
    <li class="gef-promo">...</li>
  </ul>
</aside>
```

### The promo itself

The most important thing to remember about **Promo** components is they have a single purpose: to promote another part of the BBC's services; a site, news story, television programme etc. **Promos** are differentiated from [**Cards**](../cards) in that they only have one piece of functionality: a link to the promoted content. If you intend to include functionality _in situ_, such as a video player, use a **Card** instead.

#### The headline link

The **Promo** must contain a link as its main label (or 'headline'). The wording of this link should resemble that of the target page's `<title>` and `<h1>`. This consistency aids cognitive accessibility and improves <abbr title="search engine optimization">SEO</abbr>[^4].

```html
<div class="gef-promo">
  <div class="gef-promo__content">
    <a class="gef-promo__headline" href="path/to/content">University Challenge</a>
  </div>
</div>
```

::: info Headings in headlines
Unlike **Cards**, **Promos** do not need to have a heading as their title/headline. The complementary landmark and/or list markup is deemed sufficient for providing a semantic structure. **Cards** take headings because they represent self-sufficient content and functionality belonging to the document outline, whereas **Promos** are merely navigation cues.
:::

#### Images

Frequently, an image is used to help promote the **Promo's** target content. This is the only content permitted _before_ the link in the source.

```html
<div class="gef-promo">
  <div class="gef-promo__image">
    <img src="path/to/image" alt="">
  </div>
  <div class="gef-promo__content">
    <a class="gef-promo__headline" href="path/to/content">University Challenge</a>
  </div>
</div>
```

The image may or may not contain `alt` text. If the headline and/or supporting text (where present) sufficiently describes the promoted content, and the image adds nothing salient, use `alt=""`. If the image conveys important information missing from the **Promo** text, provide an appropriate value. 

The image must _not_ be inside its own link, whether it contains `alt` text or otherwise. This would represent an unnecessary and redundant keyboard tab stop.

#### Media indication

You can indicate information about the media being promoted, if relevant. This is the job of the `class="gef-promo__indicator"` element, found inside `class="gef-promo__image"`.

```html
<div class="gef-promo">
  <div class="gef-promo__image">
    <img src="path/to/image" alt="">
    <div class="gef-promo__indicator" aria-hidden="true">
      <svg class="gel-icon gel-icon--text" focusable="false">
        <use xlink:href="{{site.basedir}}static/images/gel-icons-all.svg#gel-icon-play"></use>
      </svg>
      <span class="gef-promo__indicator-text">04:35</span>
    </div>
  </div>
  <div class="gef-promo__content">
    <a class="gef-promo__headline" href="path/to/content">
      University Challenge
      <span class="gef-sr">Video, 4 minutes and 35 seconds</span>
    </a>
  </div>
</div>
```

Importantly, the `class="gef-promo__indicator"` is hidden from assistive technologies with `aria-hidden="true"`. This is because it would not make sense encountered before the headline. Append a readable version of the information in a visually hidden span after the main headline text (_"Video, 4 minutes and 35 seconds"_ in the example). 

#### Description

If present, the description (a couple of sentences; no more) should appear after the headline and before the metadata (see the following example). Media indication is omitted from the following example for brevity. 

```html
<div class="gef-promo">
  <div class="gef-promo__image">
    <img src="path/to/image" alt="">
  </div>
  <div class="gef-promo__content">
    <a class="gef-promo__headline" href="path/to/content">University Challenge</a>
    <p>It is the first of the semi-finals in the Christmas quiz for graduates.</p>
  </div>
</div>
```

#### Metadata

The [**Metadata strip**](../metadata-strips) is described as its own component. It provides metadata in key value pairs, using a description list (`<dl>`).

```html
<div class="gef-promo">
  <div class="gef-promo__image">
    <img src="path/to/image" alt="">
  </div>
  <div class="gef-promo__content">
    <a class="gef-promo__headline" href="path/to/content">University Challenge</a>
    <p>It is the first of the semi-finals in the Christmas quiz for graduates.</p>
    <dl class="gef-metadata-strip">
      <div>
        <dt class="vh">Published:</dt>
        <dd>
          <span aria-hidden="true">
            <svg class="gel-icon gel-icon--text" focusable="false">
              <use xlink:href="path/to/gel-icons-all.svg#gel-icon-duration"></use>
            </svg>
            1m
          </span>
          <span class="vh">1 minute ago</span>
        </dd>
      </div>
      <div>
        <dt class="vh">From:</dt>
        <dd>
          <a href="link/to/category">UK</a>
        </dd>
      </div>
    </dl>
  </div>
</div>
```

## Recommended layout

A group of Promos in a set should share the same height. This is possible by making the parent (`class="gel-promos"`; `<ul>` if there are multiple **Promos** or a simple `<div>` if there is just one) a CSS Grid context. It's important there is a fallback, hence `display: inline-block` and `max-width` above the `@supports` block.

```css
.gef-promos > * {
  display: inline-block;
  max-width: 266px;
}

@supports (display: grid) {
  .gef-promos {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(266px, 1fr));
    grid-gap: 1rem;
  }
  
  .gef-promos > * {
    max-width: none;
  }
}
```

The appearance of each promo is improved by distributing the metadata (if present) to the bottom of the container. This is possible by making the **Promo** and its nested `class="gef-promo__content"` element Flexbox contexts and giving the metadata element `margin-top: auto`.

```css
.gef-promo {
  display: flex;
  flex-direction: column;
}

.gef-promo__content {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
}

.gef-promo__content .gef-metadata-strip {
  margin-top: auto;
}
```

### The image

The image will need to fit the available space, regardless of the Promo's dimensions (which are likely to change across breakpoints) without distorting. This is possible by setting the desired height of the image box and using the `object-fit` property:

```css
@supports (object-fit: cover) {
  .gef-promo__image img {
    width: 100%;
    object-fit: cover;
  }
}
```

::: info Support for object-fit
At the time of writing, the `object-fit` property is supported everywhere but Internet Explorer. The code uses `@supports` and falls back to a 'letterboxed' style using `text-align: center` and a `background-color`:

```css
.gef-promo__image {
  text-align: center;
  background-color: $gel-color--tundora; 
}
```
:::

### Horizontal promos

In the [Reference implementation](#reference-implementation), a horizontal configuration (with the image to the left of the text content) can be achieved by placing the `gel-promo--horizontal` class on the `gel-promo` element. This change's the element's flex-direction.

```css
.gef-promo.gef-promo--horizontal {
  flex-wrap: wrap;
  flex-direction: row;
}
```

The `flex-wrap: wrap` declaration ensures the image is _only_ placed to the side where there is room. The `gef-promo__image` and `gef-promo__content` elements are not permitted to become smaller than the `266px` threshold of the vertical **Promo** counterparts. At this point, wrapping occurs and the horizontal **Promo** displays as a vertical one.

```css
.gef-promo.gef-promo--horizontal .gef-promo__image {
  flex: 1;
  min-width: 266px;
}

.gef-promo.gef-promo--horizontal .gef-promo__content {
  flex: 999; /* Take up all but 266px where adjacent */
  min-width: 266px;
}
```

In a grid context, **Promos** with the class `gel-promo--horizontal` are directed to take up two columns of the grid wherever they are placed.

```css
.gef-promo.gef-promo--horizontal {
  grid-column: span 2;
}
```

### Focus styles

A `text-decoration` focus style is recommended for the headline link, paired with its hover style. To make focusing the card and its headline clearer, an additional `:focus-within` style can be added to the card itself.

```css
.gef-promo__headline:hover,
.gef-promo__headline:focus {
  outline: none;
  text-decoration: underline;
}

.gef-promo:focus-within {
  outline: 0.25rem solid;
}
```

### High contrast

How the component looks with a [Windows High Contrast Mode](https://support.microsoft.com/en-gb/help/13862/windows-use-high-contrast-mode) theme active. 

![Borders on all sides mark out the shape of the Promo]({{site.basedir}}static/images/hcm_masthead.png)

Transparent borders are applied on all sides. These become visible when Windows HCM is active, and define the shape of the Promo in the absence of the `background-color`:

```css
.gef-promo {
  background-color: $gel-color--alto;
  border: 2px solid transparent; /* for high contrast mode */
}
```

## Recommended behaviour

**Promo** interaction should be ergonomic for mouse, touch, keyboard, and screen reader users. For mouse and touch users, the whole **Promo** should be clickable as one link. This should be achieved without relying on either of the following:

1. **Multiple, duplicated links:** Linking each of the constituent elements produces multiple and redundant tab stops, impeding keyboard navigation[^6].
2. **A wrapper link:** Placing all of the **Promo's** content inside a link produces a verbose, confusing and/or truncated link label[^7] (which is liable to affect both SEO and, more importantly, screen reader experience).

Instead, the headline link's pseudo-content is positioned _over_ the entire **Promo**. 

```css
.gef-promo__headline::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
```

This leaves one piece of unfinished business: any links appearing after the headline are now not clickable. This is remedied by raising these links over the pseudo-content with `position: relative`.

```css
.gef-promo a:not(.gef-promo__headline) {
  position: relative;
}
```

::: alert Supplementary links
The headline link (`.gef-promo__headline`) is the primary purpose of the **Promo**. Although the **Metadata strip** may contain links (to category pages in the example implementation to follow) supplementary links should generally be omitted.
:::

## Example implementation

::: alert Important
Reference implementations are intended to demonstrate **what needs to be achieved**, but not necessarily how to achieve it. That would depend on the technology stack you are working with. The HTML semantics, layout, and behaviour of your implementation must conform to the reference implementation. Your JS framework, CSS methodology, and—most likely—content will differ.
:::

<include src="components/demos/promos.html">

<cta label="Open in new window" href="../demos/promos/">

## Related research

This component was originally developed and tested at the BBC in a prototype of the BBC Homepage. During user research we tested with X users, including subjects with a variety of impairments and a range of digital skills. You can read more about our research and findings on [the project Wiki page, hosted on GitHub](#linktocome).

### Further reading, elsewhere on the Web

[^1]: Complementary Landmark — W3C, <https://www.w3.org/TR/wai-aria-practices/examples/landmarks/complementary.html>
[^2]: How to structure headings for web accessibility — Nomensa, <https://www.nomensa.com/blog/2017/how-structure-headings-web-accessibility>
[^3]: "Basic screen reader commands for accessibility testing" by Léonie Watson, <https://developer.paciellogroup.com/blog/2015/01/basic-screen-reader-commands-for-accessibility-testing/>
[^4]: How To Write Page Titles For Google & Other Search Engines in 2018, <https://www.hobo-web.co.uk/title-tags/#page-titles-example-use>
[^5]: `object-fit` (caniuse data), <https://caniuse.com/#feat=object-fit>
[^6]: Keyboard Accessibility — WebAIM, <https://webaim.org/techniques/keyboard/>
[^7]: Accessibility and HTML5 Block Links — <https://simplyaccessible.com/article/html5-block-links/>
