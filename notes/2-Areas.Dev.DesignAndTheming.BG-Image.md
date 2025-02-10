---
id: s8juh7m0mi4t51lol7fn9tj
title: BG-Image
desc: ''
updated: 1733757978695
created: 1733757461036
---

# Background Image

The background-image CSS property sets one or more background images on an element.

## Baseline

Widely available. This feature is well established and works across many devices and browser versions. It’s been available across browsers since July 2015.

- [Learn more](https://developer.mozilla.org/en-US/docs/Glossary/Baseline/Compatibility)
- [See full compatibility](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#browser_compatibility)
- [Report feedback](https://survey.alchemer.com/s3/7634825/MDN-baseline-feedback?page=%2Fen-US%2Fdocs%2FWeb%2FCSS%2Fbackground-image&level=high)

The **`background-image`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) property sets one or more background images on an element.

## [Try it](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#try_it)

<iframe class="interactive is-default-height" height="200" src="https://interactive-examples.mdn.mozilla.net/pages/css/background-image.html" title="MDN Web Docs Interactive Example" allow="clipboard-write" loading="lazy"></iframe>

The background images are drawn on stacking context layers on top of each other. The first layer specified is drawn as if it is closest to the user. The [borders](https://developer.mozilla.org/en-US/docs/Web/CSS/border) of the element are then drawn on top of them, and the [`background-color`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-color) is drawn beneath them. How the images are drawn relative to the box and its borders is defined by the [`background-clip`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip) and [`background-origin`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-origin) CSS properties. If a specified image cannot be drawn (for example, when the file denoted by the specified URI cannot be loaded), browsers handle it as they would a `none` value.

**Note:** Even if the images are opaque and the color won't be displayed in normal circumstances, web developers should always specify a [`background-color`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-color). If the images cannot be loaded—for instance, when the network is down—the background color will be used as a fallback.

## [Syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#syntax)

```css
/* single image */
background-image: linear-gradient(black, white);
background-image: url("cat-front.png");

/* multiple images */
background-image: radial-gradient(circle, #0000 45%, #000f 48%), radial-gradient(ellipse farthest-corner, #fc1c14 20%, #cf15cf 80%);

/* Global values */
background-image: inherit;
background-image: initial;
background-image: revert;
background-image: revert-layer;
background-image: unset;
```

Each background image is specified either as the keyword `none` or as an [`<image>`](https://developer.mozilla.org/en-US/docs/Web/CSS/image) value. To specify multiple background images, supply multiple values, separated by a comma.

### [Values](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#values)

- [`none`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#none): Is a keyword denoting the absence of images.
- [`<image>`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#image): Is an [`<image>`](https://developer.mozilla.org/en-US/docs/Web/CSS/image) denoting the image to display. There can be several of them, separated by commas, as [multiple backgrounds](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders/Using_multiple_backgrounds) are supported.

## [Accessibility](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#accessibility)

Browsers do not provide any special information on background images to assistive technology. This is important primarily for screen readers, as a screen reader will not announce its presence and therefore convey nothing to its users. If the image contains information critical to understanding the page's overall purpose, it is better to describe it semantically in the document.

- [MDN Understanding WCAG, Guideline 1.1 explanations](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Understanding_WCAG/Perceivable#guideline_1.1_%E2%80%94_providing_text_alternatives_for_non-text_content)
- [Understanding Success Criterion 1.1.1 | W3C Understanding WCAG 2.0](https://www.w3.org/TR/2016/NOTE-UNDERSTANDING-WCAG20-20161007/text-equiv-all.html)

Additionally, it is important to ensure that the contrast ratio between the background image and the foreground text is high enough that people with low vision can read the page content. Color contrast ratio is determined by comparing the luminance of the text and background color values. To meet [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/), a ratio of 4.5:1 is required for body text content and 3:1 for larger text such as headings. Large text is defined as 24px or larger, or [bolded](https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight) 18.66px or larger.

- [WebAIM: Color Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Understanding WCAG, Guideline 1.4 explanation](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Understanding_WCAG/Perceivable#guideline_1.4_make_it_easier_for_users_to_see_and_hear_content_including_separating_foreground_from_background)
- [Understanding Success Criterion 1.4.3 | Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html), W3C (2023)

## [Formal definition](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#formal_definition)

| Property | Value |
| --- | --- |
| [Initial value](https://developer.mozilla.org/en-US/docs/Web/CSS/initial_value) | `none` |
| Applies to | all elements. It also applies to [`::first-letter`](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-letter) and [`::first-line`](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-line). |
| [Inherited](https://developer.mozilla.org/en-US/docs/Web/CSS/Inheritance) | no |
| [Computed value](https://developer.mozilla.org/en-US/docs/Web/CSS/computed_value) | as specified, but with [`<url>`](https://developer.mozilla.org/en-US/docs/Web/CSS/url_value) values made absolute |
| [Animation type](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) | discrete |

## [Formal syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#formal_syntax)

```css
background-image = <bg-image>#

<bg-image> = <image> | none

<image> = <url> | <gradient>

<url> = <url()> | <src()>

<url()> = url(<string><url-modifier>*)

<src()> = src(<string><url-modifier>*)
```

## [Examples](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#examples)

### [Layering background images](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image#layering_background_images)

Note that the star image is partially transparent and is layered over the cat image.

#### HTML

```html
<div>
  <p class="cats-and-stars">This paragraph is full of cats<br>and stars.</p>
  <p>This paragraph is not.</p>
  <p class="cats-and-stars">Here are more cats for you.<br>Look at them!</p>
  <p>And no more.</p>
</div>
```

#### CSS

```css
p {
  font-weight: bold;
  font-size: 1.5em;
  color: white;
  text-shadow: 0.07em 0.07em 0.05em black;
  background-image: none;
  background-color: transparent;
}

div {
  background-image: url("mdn_logo_only_color.png");
}

.cats-and-stars {
  background-image: url("star-transparent.gif"), url("cat-front.png");
  background-color: transparent;
}
