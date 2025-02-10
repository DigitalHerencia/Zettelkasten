---
id: f3sggopzrr9yjprw08mdcxk
title: Image
desc: ''
updated: 1733756475271
created: 1733756424410
---


# &lt;Image&gt;

* * *

This API reference will help you understand how to use [props](https://nextjs.org/docs/app/api-reference/components/image#props) and [configuration options](https://nextjs.org/docs/app/api-reference/components/image#configuration-options) available for the Image Component. For features and usage, please see the [Image Component](https://nextjs.org/docs/app/building-your-application/optimizing/images) page.

```ts
import Image from 'next/image';

export default function Page() {
  return (
    <Image
      src="/profile.png"
      width={500}
      height={500}
      alt="Picture of the author"
    />
  );
}

```

## [Props<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#props)

Here's a summary of the props available for the Image Component:

| Prop | Example | Type | Status |
| --- | --- | --- | --- |
| [`src`](https://nextjs.org/docs/app/api-reference/components/image#src) | `src="/profile.png"` | String | Required |
| [`width`](https://nextjs.org/docs/app/api-reference/components/image#width) | `width={500}` | Integer (px) | Required |
| [`height`](https://nextjs.org/docs/app/api-reference/components/image#height) | `height={500}` | Integer (px) | Required |
| [`alt`](https://nextjs.org/docs/app/api-reference/components/image#alt) | `alt="Picture of the author"` | String | Required |
| [`loader`](https://nextjs.org/docs/app/api-reference/components/image#loader) | `loader={imageLoader}` | Function | - |
| [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) | `fill={true}` | Boolean | - |
| [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) | `sizes="(max-width: 768px) 100vw, 33vw"` | String | - |
| [`quality`](https://nextjs.org/docs/app/api-reference/components/image#quality) | `quality={80}` | Integer (1-100) | - |
| [`priority`](https://nextjs.org/docs/app/api-reference/components/image#priority) | `priority={true}` | Boolean | - |
| [`placeholder`](https://nextjs.org/docs/app/api-reference/components/image#placeholder) | `placeholder="blur"` | String | - |
| [`style`](https://nextjs.org/docs/app/api-reference/components/image#style) | `style={{objectFit: "contain"}}` | Object | - |
| [`onLoadingComplete`](https://nextjs.org/docs/app/api-reference/components/image#onloadingcomplete) | `onLoadingComplete={img => done())}` | Function | Deprecated |
| [`onLoad`](https://nextjs.org/docs/app/api-reference/components/image#onload) | `onLoad={event => done())}` | Function | - |
| [`onError`](https://nextjs.org/docs/app/api-reference/components/image#onerror) | `onError(event => fail()}` | Function | - |
| [`loading`](https://nextjs.org/docs/app/api-reference/components/image#loading) | `loading="lazy"` | String | - |
| [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl) | `blurDataURL="data:image/jpeg..."` | String | - |
| [`overrideSrc`](https://nextjs.org/docs/app/api-reference/components/image#overridesrc) | `overrideSrc="/seo.png"` | String | - |

## [Required Props<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#required-props)

The Image Component requires the following properties: `src`, `alt`, `width` and `height` (or `fill`).

```ts
import Image from 'next/image'

export default function Page() {
  return (
    <div>
      <Image src="/profile.png" width={500} height={500} alt="Picture of the author" />
    </div>
  )
}

```

### [`src`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#src)

Must be one of the following:

- A [statically imported](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) image file
- A path string. This can be either an absolute external URL, or an internal path depending on the [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) prop.

When using the default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader), also consider the following for source images:

- When src is an external URL, you must also configure [remotePatterns](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns)
- When src is [animated](https://nextjs.org/docs/app/api-reference/components/image#animated-images) or not a known format (JPEG, PNG, WebP, AVIF, GIF, TIFF) the image will be served as-is
- When src is SVG format, it will be blocked unless [`unoptimized`](https://nextjs.org/docs/app/api-reference/components/image#unoptimized) or [`dangerouslyAllowSVG`](https://nextjs.org/docs/app/api-reference/components/image#dangerouslyallowsvg) is enabled

### [`width`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#width)

The `width` property represents the *intrinsic* image width in pixels. This property is used to infer the correct aspect ratio of the image and avoid layout shift during loading. It does not determine the rendered size of the image, which is controlled by CSS, similar to the `width` attribute in the HTML `<img>` tag.

Required, except for [statically imported images](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) or images with the [`fill` property](https://nextjs.org/docs/app/api-reference/components/image#fill).

### [`height`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#height)

The `height` property represents the *intrinsic* image height in pixels. This property is used to infer the correct aspect ratio of the image and avoid layout shift during loading. It does not determine the rendered size of the image, which is controlled by CSS, similar to the `height` attribute in the HTML `<img>` tag.

Required, except for [statically imported images](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) or images with the [`fill` property](https://nextjs.org/docs/app/api-reference/components/image#fill).

> 
> **Good to know:**
> 
> - Combined, both `width` and `height` properties are used to determine the aspect ratio of the image which used by browsers to reserve space for the image before it loads.
> - The intrinsic size does not always mean the rendered size in the browser, which will be determined by the parent container. For example, if the parent container is smaller than the intrinsic size, the image will be scaled down to fit the container.
> - You can use the [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) property when the width and height are unknown.
> 

### [`alt`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#alt)

The `alt` property is used to describe the image for screen readers and search engines. It is also the fallback text if images have been disabled or an error occurs while loading the image.

It should contain text that could replace the image [without changing the meaning of the page<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://html.spec.whatwg.org/multipage/images.html#general-guidelines). It is not meant to supplement the image and should not repeat information that is already provided in the captions above or below the image.

If the image is [purely decorative<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://html.spec.whatwg.org/multipage/images.html#a-purely-decorative-image-that-doesn't-add-any-information) or [not intended for the user<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://html.spec.whatwg.org/multipage/images.html#an-image-not-intended-for-the-user), the `alt` property should be an empty string (`alt=""`).

[Learn more<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://html.spec.whatwg.org/multipage/images.html#alt)

## [Optional Props<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#optional-props)

The `<Image />` component accepts a number of additional properties beyond those which are required. This section describes the most commonly-used properties of the Image component. Find details about more rarely-used properties in the [Advanced Props](https://nextjs.org/docs/app/api-reference/components/image#advanced-props) section.

### [`loader`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#loader)

A custom function used to resolve image URLs.

A `loader` is a function returning a URL string for the image, given the following parameters:

- [`src`](https://nextjs.org/docs/app/api-reference/components/image#src)
- [`width`](https://nextjs.org/docs/app/api-reference/components/image#width)
- [`quality`](https://nextjs.org/docs/app/api-reference/components/image#quality)

Here is an example of using a custom loader:

<button aria-label="Copy code" class="code-block_copyButton__uo5Yu code-block_copyFloatingButton__PsMvB" type="button"><svg data-testid="geist-icon" height="16" stroke-linejoin="round" viewbox="0 0 16 16" width="16" aria-hidden="true"><path fill-rule="evenodd" clip-rule="evenodd" d="M2.75 0.5C1.7835 0.5 1 1.2835 1 2.25V9.75C1 10.7165 1.7835 11.5 2.75 11.5H3.75H4.5V10H3.75H2.75C2.61193 10 2.5 9.88807 2.5 9.75V2.25C2.5 2.11193 2.61193 2 2.75 2H8.25C8.38807 2 8.5 2.11193 8.5 2.25V3H10V2.25C10 1.2835 9.2165 0.5 8.25 0.5H2.75ZM7.75 4.5C6.7835 4.5 6 5.2835 6 6.25V13.75C6 14.7165 6.7835 15.5 7.75 15.5H13.25C14.2165 15.5 15 14.7165 15 13.75V6.25C15 5.2835 14.2165 4.5 13.25 4.5H7.75ZM7.5 6.25C7.5 6.11193 7.61193 6 7.75 6H13.25C13.3881 6 13.5 6.11193 13.5 6.25V13.75C13.5 13.8881 13.3881 14 13.25 14H7.75C7.61193 14 7.5 13.8881 7.5 13.75V6.25Z" fill="currentColor"></path></svg><svg data-testid="geist-icon" height="16" stroke-linejoin="round" viewbox="0 0 16 16" width="16" aria-hidden="true"><path fill-rule="evenodd" clip-rule="evenodd" d="M15.5607 3.99999L15.0303 4.53032L6.23744 13.3232C5.55403 14.0066 4.44599 14.0066 3.76257 13.3232L4.2929 12.7929L3.76257 13.3232L0.969676 10.5303L0.439346 9.99999L1.50001 8.93933L2.03034 9.46966L4.82323 12.2626C4.92086 12.3602 5.07915 12.3602 5.17678 12.2626L13.9697 3.46966L14.5 2.93933L15.5607 3.99999Z" fill="currentColor"></path></svg></button>

```ts
'use client'
import Image from 'next/image'

const imageLoader = ({ src, width, quality }) => {
  return `https://example.com/${src}?w=${width}&q=${quality || 75}`
}

export default function Page() {
  return (
    <Image
      loader={imageLoader}
      src="me.png"
      alt="Picture of the author"
      width={500}
      height={500}
    />
  )
}

```

> 
> **Good to know**: Using props like `loader`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

Alternatively, you can use the [loaderFile](https://nextjs.org/docs/app/api-reference/components/image#loaderfile) configuration in `next.config.js` to configure every instance of `next/image` in your application, without passing a prop.

### [`fill`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#fill)

```ts

fill={true} // {true} | {false}

```

A boolean that causes the image to fill the parent element, which is useful when the [`width`](https://nextjs.org/docs/app/api-reference/components/image#width) and [`height`](https://nextjs.org/docs/app/api-reference/components/image#height) are unknown.

The parent element *must* assign `position: "relative"`, `position: "fixed"`, or `position: "absolute"` style.

By default, the img element will automatically be assigned the `position: "absolute"` style.

If no styles are applied to the image, the image will stretch to fit the container. You may prefer to set `object-fit: "contain"` for an image which is letterboxed to fit the container and preserve aspect ratio.

Alternatively, `object-fit: "cover"` will cause the image to fill the entire container and be cropped to preserve aspect ratio.

For more information, see also:

- [`position`<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/CSS/position)
- [`object-fit`<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/CSS/object-fit)
- [`object-position`<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/CSS/object-position)

### [`sizes`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#sizes)

A string, similar to a media query, that provides information about how wide the image will be at different breakpoints. The value of `sizes` will greatly affect performance for images using [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) or which are [styled to have a responsive size](https://nextjs.org/docs/app/api-reference/components/image#responsive-images).

The `sizes` property serves two important purposes related to image performance:

- First, the value of `sizes` is used by the browser to determine which size of the image to download, from `next/image`'s automatically generated `srcset`. When the browser chooses, it does not yet know the size of the image on the page, so it selects an image that is the same size or larger than the viewport. The `sizes` property allows you to tell the browser that the image will actually be smaller than full screen. If you don't specify a `sizes` value in an image with the `fill` property, a default value of `100vw` (full screen width) is used.
- Second, the `sizes` property changes the behavior of the automatically generated `srcset` value. If no `sizes` value is present, a small `srcset` is generated, suitable for a fixed-size image (1x/2x/etc). If `sizes` is defined, a large `srcset` is generated, suitable for a responsive image (640w/750w/etc). If the `sizes` property includes sizes such as `50vw`, which represent a percentage of the viewport width, then the `srcset` is trimmed to not include any values which are too small to ever be necessary.

For example, if you know your styling will cause an image to be full-width on mobile devices, in a 2-column layout on tablets, and a 3-column layout on desktop displays, you should include a sizes property such as the following:

```ts
import Image from 'next/image';

export default function Page() {
  return (
    <div className="grid-element">
      <Image
        fill
        src="/example.png"
        sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
        alt="Example image"
      />
    </div>
  );
}

```

This example `sizes` could have a dramatic effect on performance metrics. Without the `33vw` sizes, the image selected from the server would be 3 times as wide as it needs to be. Because file size is proportional to the square of the width, without `sizes` the user would download an image that's 9 times larger than necessary.

Learn more about `srcset` and `sizes`:

- [web.dev<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://web.dev/learn/design/responsive-images/#sizes)
- [mdn<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/HTML/Element/img#sizes)

### [`quality`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#quality)

```ts
quality={75} // {number 1-100}

```

The quality of the optimized image, an integer between `1` and `100`, where `100` is the best quality and therefore largest file size. Defaults to `75`.

### [`priority`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#priority)

```ts
priority={false} // {false} | {true}

```

When true, the image will be considered high priority and [preload<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://web.dev/preload-responsive-images/). Lazy loading is automatically disabled for images using `priority`. If the [`loading`](https://nextjs.org/docs/app/api-reference/components/image#loading) property is also used and set to `lazy`, the `priority` property can't be used. The [`loading`](https://nextjs.org/docs/app/api-reference/components/image#loading) property is only meant for advanced use cases. Remove `loading` when `priority` is needed.

You should use the `priority` property on any image detected as the [Largest Contentful Paint (LCP)<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://nextjs.org/learn/seo/web-performance/lcp) element. It may be appropriate to have multiple priority images, as different images may be the LCP element for different viewport sizes.

Should only be used when the image is visible above the fold. Defaults to `false`.

### [`placeholder`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#placeholder)

```ts
placeholder = 'empty' // "empty" | "blur" | "data:image/..."

```

A placeholder to use while the image is loading. Possible values are `blur`, `empty`, or `data:image/...`. Defaults to `empty`.

When `blur`, the [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl) property will be used as the placeholder. If `src` is an object from a [static import](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) and the imported image is `.jpg`, `.png`, `.webp`, or `.avif`, then `blurDataURL` will be automatically populated, except when the image is detected to be animated.

For dynamic images, you must provide the [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl) property. Solutions such as [Plaiceholder<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://github.com/joe-bell/plaiceholder) can help with `base64` generation.

When `data:image/...`, the [Data URL<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) will be used as the placeholder while the image is loading.

When `empty`, there will be no placeholder while the image is loading, only empty space.

Try it out:

- [Demo the `blur` placeholder<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/placeholder)
- [Demo the shimmer effect with data URL `placeholder` prop<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/shimmer)
- [Demo the color effect with `blurDataURL` prop<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/color)

## [Advanced Props<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#advanced-props)

In some cases, you may need more advanced usage. The `<Image />` component optionally accepts the following advanced properties.

### [`style`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#style)

Allows passing CSS styles to the underlying image element.

```ts
const imageStyle = {
  borderRadius: '50%',
  border: '1px solid #fff',
}

export default function ProfileImage() {
  return <Image src="..." style={imageStyle} />
}

```

Remember that the required width and height props can interact with your styling. If you use styling to modify an image's width, you should also style its height to `auto` to preserve its intrinsic aspect ratio, or your image will be distorted.

### [`onLoadingComplete`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#onloadingcomplete)

```ts
'use client' <Image onLoadingComplete={(img) => console.log(img.naturalWidth)} />

```

> 
> **Warning**: Deprecated since Next.js 14 in favor of [`onLoad`](https://nextjs.org/docs/app/api-reference/components/image#onload).

A callback function that is invoked once the image is completely loaded and the [placeholder](https://nextjs.org/docs/app/api-reference/components/image#placeholder) has been removed.

The callback function will be called with one argument, a reference to the underlying `<img>` element.

> 
> **Good to know**: Using props like `onLoadingComplete`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

### [`onLoad`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#onload)

```ts
<Image onLoad={(e) => console.log(e.target.naturalWidth)} />

```

A callback function that is invoked once the image is completely loaded and the [placeholder](https://nextjs.org/docs/app/api-reference/components/image#placeholder) has been removed.

The callback function will be called with one argument, the Event which has a `target` that references the underlying `<img>` element.

> 
> **Good to know**: Using props like `onLoad`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

### [`onError`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#onerror)

```ts
 <Image onError={(e) => console.error(e.target.id)} />

```

A callback function that is invoked if the image fails to load.

> 
> **Good to know**: Using props like `onError`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

### [`loading`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#loading)

```ts
loading = 'lazy' // {lazy} | {eager}

```

The loading behavior of the image. Defaults to `lazy`.

When `lazy`, defer loading the image until it reaches a calculated distance from the viewport.

When `eager`, load the image immediately.

Learn more about the [`loading` attribute<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/HTML/Element/img#loading).

### [`blurDataURL`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl)

A [Data URL<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) to be used as a placeholder image before the `src` image successfully loads. Only takes effect when combined with [`placeholder="blur"`](https://nextjs.org/docs/app/api-reference/components/image#placeholder).

Must be a base64-encoded image. It will be enlarged and blurred, so a very small image (10px or less) is recommended. Including larger images as placeholders may harm your application performance.

Try it out:

- [Demo the default `blurDataURL` prop<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/placeholder)
- [Demo the color effect with `blurDataURL` prop<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/color)

You can also [generate a solid color Data URL<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://png-pixel.com/) to match the image.

### [`unoptimized`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#unoptimized)

```ts
unoptimized = {false} // {false} | {true}

```

When true, the source image will be served as-is instead of changing quality, size, or format. Defaults to `false`.

```ts
import Image from 'next/image'

const UnoptimizedImage = (props) => {
  return <Image {...props} unoptimized />
}

```

Since Next.js 12.3.0, this prop can be assigned to all images by updating `next.config.js` with the following configuration:

next.config.js

```js
module.exports = { images: { unoptimized: true, },}

```

### [`overrideSrc`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#overridesrc)

When providing the `src` prop to the `<Image>` component, both the `srcset` and `src` attributes are generated automatically for the resulting `<img>`.

```js
<Image src="/me.jpg" />

```

```html
<img srcset=" /_next/image?url=%2Fme.jpg&w=640&q=75 1x, /_next/image?url=%2Fme.jpg&w=828&q=75 2x " src="/_next/image?url=%2Fme.jpg&w=828&q=75"/>

```

In some cases, it is not desirable to have the `src` attribute generated and you may wish to override it using the `overrideSrc` prop.

For example, when upgrading an existing website from `<img>` to `<Image>`, you may wish to maintain the same `src` attribute for SEO purposes such as image ranking or avoiding recrawl.

```js
<Image src="/me.jpg" overrideSrc="/override.jpg" />

```

```html
<img srcset=" /_next/image?url=%2Fme.jpg&w=640&q=75 1x, /_next/image?url=%2Fme.jpg&w=828&q=75 2x " src="/override.jpg"/>

```

### [decoding<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#decoding)

A hint to the browser indicating if it should wait for the image to be decoded before presenting other content updates or not. Defaults to `async`.

Possible values are the following:

- `async` - Asynchronously decode the image and allow other content to be rendered before it completes.
- `sync` - Synchronously decode the image for atomic presentation with other content.
- `auto` - No preference for the decoding mode; the browser decides what's best.

Learn more about the [`decoding` attribute<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/HTML/Element/img#decoding).

### [Other Props<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#other-props)

Other properties on the `<Image />` component will be passed to the underlying `img` element with the exception of the following:

- `srcSet`. Use [Device Sizes](https://nextjs.org/docs/app/api-reference/components/image#devicesizes) instead.

## [Configuration Options<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#configuration-options)

In addition to props, you can configure the Image Component in `next.config.js`. The following options are available:

## [`localPatterns`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#localpatterns)

You can optionally configure `localPatterns` in your `next.config.js` file in order to allow specific paths to be optimized and block all others paths.

<svg height="17" viewbox="0 0 50 50" width="17" xmlns="http://www.w3.org/2000/svg"><path d="M 43.335938 4 L 6.667969 4 C 5.195313 4 4 5.195313 4 6.667969 L 4 43.332031 C 4 44.804688 5.195313 46 6.667969 46 L 43.332031 46 C 44.804688 46 46 44.804688 46 43.335938 L 46 6.667969 C 46 5.195313 44.804688 4 43.335938 4 Z M 27 36.183594 C 27 40.179688 24.65625 42 21.234375 42 C 18.140625 42 15.910156 39.925781 15 38 L 18.144531 36.097656 C 18.75 37.171875 19.671875 38 21 38 C 22.269531 38 23 37.503906 23 35.574219 L 23 23 L 27 23 Z M 35.675781 42 C 32.132813 42 30.121094 40.214844 29 38 L 32 36 C 32.816406 37.335938 33.707031 38.613281 35.589844 38.613281 C 37.171875 38.613281 38 37.824219 38 36.730469 C 38 35.425781 37.140625 34.960938 35.402344 34.199219 L 34.449219 33.789063 C 31.695313 32.617188 29.863281 31.148438 29.863281 28.039063 C 29.863281 25.179688 32.046875 23 35.453125 23 C 37.878906 23 39.621094 23.84375 40.878906 26.054688 L 37.910156 27.964844 C 37.253906 26.789063 36.550781 26.328125 35.453125 26.328125 C 34.335938 26.328125 33.628906 27.039063 33.628906 27.964844 C 33.628906 29.109375 34.335938 29.570313 35.972656 30.28125 L 36.925781 30.691406 C 40.171875 32.078125 42 33.496094 42 36.683594 C 42 40.117188 39.300781 42 35.675781 42 Z" fill="currentColor"></path></svg>
next.config.js

<button aria-label="Copy code" class="code-block_copyButton__uo5Yu" type="button"><svg data-testid="geist-icon" height="16" stroke-linejoin="round" viewbox="0 0 16 16" width="16" aria-hidden="true"><path fill-rule="evenodd" clip-rule="evenodd" d="M2.75 0.5C1.7835 0.5 1 1.2835 1 2.25V9.75C1 10.7165 1.7835 11.5 2.75 11.5H3.75H4.5V10H3.75H2.75C2.61193 10 2.5 9.88807 2.5 9.75V2.25C2.5 2.11193 2.61193 2 2.75 2H8.25C8.38807 2 8.5 2.11193 8.5 2.25V3H10V2.25C10 1.2835 9.2165 0.5 8.25 0.5H2.75ZM7.75 4.5C6.7835 4.5 6 5.2835 6 6.25V13.75C6 14.7165 6.7835 15.5 7.75 15.5H13.25C14.2165 15.5 15 14.7165 15 13.75V6.25C15 5.2835 14.2165 4.5 13.25 4.5H7.75ZM7.5 6.25C7.5 6.11193 7.61193 6 7.75 6H13.25C13.3881 6 13.5 6.11193 13.5 6.25V13.75C13.5 13.8881 13.3881 14 13.25 14H7.75C7.61193 14 7.5 13.8881 7.5 13.75V6.25Z" fill="currentColor"></path></svg><svg data-testid="geist-icon" height="16" stroke-linejoin="round" viewbox="0 0 16 16" width="16" aria-hidden="true"><path fill-rule="evenodd" clip-rule="evenodd" d="M15.5607 3.99999L15.0303 4.53032L6.23744 13.3232C5.55403 14.0066 4.44599 14.0066 3.76257 13.3232L4.2929 12.7929L3.76257 13.3232L0.969676 10.5303L0.439346 9.99999L1.50001 8.93933L2.03034 9.46966L4.82323 12.2626C4.92086 12.3602 5.07915 12.3602 5.17678 12.2626L13.9697 3.46966L14.5 2.93933L15.5607 3.99999Z" fill="currentColor"></path></svg></button>

    module.exports = { images: { localPatterns: [ { pathname: '/assets/images/**', search: '', }, ], },}

> 
> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `/assets/images/` and must not have a query string. Attempting to optimize any other path will respond with 400 Bad Request.

### [`remotePatterns`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns)

To protect your application from malicious users, configuration is required in order to use external images. This ensures that only external images from your account can be served from the Next.js Image Optimization API. These external images can be configured with the `remotePatterns` property in your `next.config.js` file, as shown below:

```js
    module.exports = {
      images: {
        remotePatterns: [
          {
            protocol: 'https',
            hostname: 'example.com',
            port: '',
            pathname: '/account123/**',
            search: '',
          },
        ],
      },
    };

```
> 
> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `https://example.com/account123/` and must not have a query string. Any other protocol, hostname, port, or unmatched path will respond with 400 Bad Request.

Below is an example of the `remotePatterns` property in the `next.config.js` file using a wildcard pattern in the `hostname`:

```js
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: '**.example.com',
        port: '',
        search: '',
      },
    ],
  },
};

```

> 
> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `https://img1.example.com` or `https://me.avatar.example.com` or any number of subdomains. It cannot have a port or query string. Any other protocol or unmatched hostname will respond with 400 Bad Request.

Wildcard patterns can be used for both `pathname` and `hostname` and have the following syntax:

- `*` match a single path segment or subdomain
- `**` match any number of path segments at the end or subdomains at the beginning

The `**` syntax does not work in the middle of the pattern.

> 
> **Good to know**: When omitting `protocol`, `port`, `pathname`, or `search` then the wildcard `**` is implied. This is not recommended because it may allow malicious actors to optimize urls you did not intend.

Below is an example of the `remotePatterns` property in the `next.config.js` file using `search`:

```js
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'assets.example.com',
        search: '?v=1727111025337',
      },
    ],
  },
};

```

> 
> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `https://assets.example.com` and must have the exact query string `?v=1727111025337`. Any other protocol or query string will respond with 400 Bad Request.

### [`domains`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#domains)

> 
> **Warning**: Deprecated since Next.js 14 in favor of strict [`remotePatterns`](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns) in order to protect your application from malicious users. Only use `domains` if you own all the content served from the domain.

Similar to [`remotePatterns`](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns), the `domains` configuration can be used to provide a list of allowed hostnames for external images.

However, the `domains` configuration does not support wildcard pattern matching and it cannot restrict protocol, port, or pathname.

Below is an example of the `domains` property in the `next.config.js` file:

<svg height="17" viewbox="0 0 50 50" width="17" xmlns="http://www.w3.org/2000/svg"><path d="M 43.335938 4 L 6.667969 4 C 5.195313 4 4 5.195313 4 6.667969 L 4 43.332031 C 4 44.804688 5.195313 46 6.667969 46 L 43.332031 46 C 44.804688 46 46 44.804688 46 43.335938 L 46 6.667969 C 46 5.195313 44.804688 4 43.335938 4 Z M 27 36.183594 C 27 40.179688 24.65625 42 21.234375 42 C 18.140625 42 15.910156 39.925781 15 38 L 18.144531 36.097656 C 18.75 37.171875 19.671875 38 21 38 C 22.269531 38 23 37.503906 23 35.574219 L 23 23 L 27 23 Z M 35.675781 42 C 32.132813 42 30.121094 40.214844 29 38 L 32 36 C 32.816406 37.335938 33.707031 38.613281 35.589844 38.613281 C 37.171875 38.613281 38 37.824219 38 36.730469 C 38 35.425781 37.140625 34.960938 35.402344 34.199219 L 34.449219 33.789063 C 31.695313 32.617188 29.863281 31.148438 29.863281 28.039063 C 29.863281 25.179688 32.046875 23 35.453125 23 C 37.878906 23 39.621094 23.84375 40.878906 26.054688 L 37.910156 27.964844 C 37.253906 26.789063 36.550781 26.328125 35.453125 26.328125 C 34.335938 26.328125 33.628906 27.039063 33.628906 27.964844 C 33.628906 29.109375 34.335938 29.570313 35.972656 30.28125 L 36.925781 30.691406 C 40.171875 32.078125 42 33.496094 42 36.683594 C 42 40.117188 39.300781 42 35.675781 42 Z" fill="currentColor"></path></svg>
next.config.js

<button aria-label="Copy code" class="code-block_copyButton__uo5Yu" type="button"><svg data-testid="geist-icon" height="16" stroke-linejoin="round" viewbox="0 0 16 16" width="16" aria-hidden="true"><path fill-rule="evenodd" clip-rule="evenodd" d="M2.75 0.5C1.7835 0.5 1 1.2835 1 2.25V9.75C1 10.7165 1.7835 11.5 2.75 11.5H3.75H4.5V10H3.75H2.75C2.61193 10 2.5 9.88807 2.5 9.75V2.25C2.5 2.11193 2.61193 2 2.75 2H8.25C8.38807 2 8.5 2.11193 8.5 2.25V3H10V2.25C10 1.2835 9.2165 0.5 8.25 0.5H2.75ZM7.75 4.5C6.7835 4.5 6 5.2835 6 6.25V13.75C6 14.7165 6.7835 15.5 7.75 15.5H13.25C14.2165 15.5 15 14.7165 15 13.75V6.25C15 5.2835 14.2165 4.5 13.25 4.5H7.75ZM7.5 6.25C7.5 6.11193 7.61193 6 7.75 6H13.25C13.3881 6 13.5 6.11193 13.5 6.25V13.75C13.5 13.8881 13.3881 14 13.25 14H7.75C7.61193 14 7.5 13.8881 7.5 13.75V6.25Z" fill="currentColor"></path></svg><svg data-testid="geist-icon" height="16" stroke-linejoin="round" viewbox="0 0 16 16" width="16" aria-hidden="true"><path fill-rule="evenodd" clip-rule="evenodd" d="M15.5607 3.99999L15.0303 4.53032L6.23744 13.3232C5.55403 14.0066 4.44599 14.0066 3.76257 13.3232L4.2929 12.7929L3.76257 13.3232L0.969676 10.5303L0.439346 9.99999L1.50001 8.93933L2.03034 9.46966L4.82323 12.2626C4.92086 12.3602 5.07915 12.3602 5.17678 12.2626L13.9697 3.46966L14.5 2.93933L15.5607 3.99999Z" fill="currentColor"></path></svg></button>

    module.exports = { images: { domains: ['assets.acme.com'], },}

### [`loaderFile`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#loaderfile)

If you want to use a cloud provider to optimize images instead of using the Next.js built-in Image Optimization API, you can configure the `loaderFile` in your `next.config.js` like the following:

```js
module.exports = {
  images: {
    loader: 'custom',
    loaderFile: './my/image/loader.js',
  },
}

```
This must point to a file relative to the root of your Next.js application. The file must export a default function that returns a string, for example:

```js
//my/image/loader.js
'use client'
export default function myImageLoader({ src, width, quality }) {
  return `https://example.com/${src}?w=${width}&q=${quality || 75}`
}

```

Alternatively, you can use the [`loader` prop](https://nextjs.org/docs/app/api-reference/components/image#loader) to configure each instance of `next/image`.

Examples:

- [Custom Image Loader Configuration](https://nextjs.org/docs/app/api-reference/next-config-js/images#example-loader-configuration)

> 
> **Good to know**: Customizing the image loader file, which accepts a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

## [Advanced<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#advanced)

The following configuration is for advanced use cases and is usually not necessary. If you choose to configure the properties below, you will override any changes to the Next.js defaults in future updates.

### [`deviceSizes`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#devicesizes)

If you know the expected device widths of your users, you can specify a list of device width breakpoints using the `deviceSizes` property in `next.config.js`. These widths are used when the `next/image` component uses [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) prop to ensure the correct image is served for user's device.

If no configuration is provided, the default below is used.

```js
module.exports = { images: { deviceSizes: [640, 750, 828, 1080, 1200, 1920, 2048, 3840], },}

```

### [`imageSizes`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#imagesizes)

You can specify a list of image widths using the `images.imageSizes` property in your `next.config.js` file. These widths are concatenated with the array of [device sizes](https://nextjs.org/docs/app/api-reference/components/image#devicesizes) to form the full array of sizes used to generate image [srcset<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/API/HTMLImageElement/srcset)s.

The reason there are two separate lists is that imageSizes is only used for images which provide a [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) prop, which indicates that the image is less than the full width of the screen. **Therefore, the sizes in imageSizes should all be smaller than the smallest size in deviceSizes.**

If no configuration is provided, the default below is used.

```js
module.exports = { images: { imageSizes: [16, 32, 48, 64, 96, 128, 256, 384], },}

```

### [`formats`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#formats)

The default [Image Optimization API](https://nextjs.org/docs/app/api-reference/components/image#loader) will automatically detect the browser's supported image formats via the request's `Accept` header in order to determine the best output format.

If the `Accept` header matches more than one of the configured formats, the first match in the array is used. Therefore, the array order matters. If there is no match (or the source image is [animated](https://nextjs.org/docs/app/api-reference/components/image#animated-images)), the Image Optimization API will fallback to the original image's format.

If no configuration is provided, the default below is used.

```js
module.exports = { images: { formats: ['image/webp'], },}

```

You can enable AVIF support and still fallback to WebP with the following configuration.

```js
module.exports = { images: { formats: ['image/avif', 'image/webp'], },}

```

> 
> **Good to know**:
> 
> - AVIF generally takes 50% longer to encode but it compresses 20% smaller compared to WebP. This means that the first time an image is requested, it will typically be slower and then subsequent requests that are cached will be faster.
> - If you self-host with a Proxy/CDN in front of Next.js, you must configure the Proxy to forward the `Accept` header.
> 

## [Caching Behavior<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#caching-behavior)

The following describes the caching algorithm for the default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader). For all other loaders, please refer to your cloud provider's documentation.

Images are optimized dynamically upon request and stored in the `<distDir>/cache/images` directory. The optimized image file will be served for subsequent requests until the expiration is reached. When a request is made that matches a cached but expired file, the expired image is served stale immediately. Then the image is optimized again in the background (also called revalidation) and saved to the cache with the new expiration date.

The cache status of an image can be determined by reading the value of the `x-nextjs-cache` response header. The possible values are the following:

- `MISS` - the path is not in the cache (occurs at most once, on the first visit)
- `STALE` - the path is in the cache but exceeded the revalidate time so it will be updated in the background
- `HIT` - the path is in the cache and has not exceeded the revalidate time

The expiration (or rather Max Age) is defined by either the [`minimumCacheTTL`](https://nextjs.org/docs/app/api-reference/components/image#minimumcachettl) configuration or the upstream image `Cache-Control` header, whichever is larger. Specifically, the `max-age` value of the `Cache-Control` header is used. If both `s-maxage` and `max-age` are found, then `s-maxage` is preferred. The `max-age` is also passed-through to any downstream clients including CDNs and browsers.

- You can configure [`minimumCacheTTL`](https://nextjs.org/docs/app/api-reference/components/image#minimumcachettl) to increase the cache duration when the upstream image does not include `Cache-Control` header or the value is very low.
- You can configure [`deviceSizes`](https://nextjs.org/docs/app/api-reference/components/image#devicesizes) and [`imageSizes`](https://nextjs.org/docs/app/api-reference/components/image#imagesizes) to reduce the total number of possible generated images.
- You can configure [formats](https://nextjs.org/docs/app/api-reference/components/image#formats) to disable multiple formats in favor of a single image format.

### [`minimumCacheTTL`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#minimumcachettl)

You can configure the Time to Live (TTL) in seconds for cached optimized images. In many cases, it's better to use a [Static Image Import](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) which will automatically hash the file contents and cache the image forever with a `Cache-Control` header of `immutable`.

```js
module.exports = { images: { minimumCacheTTL: 60, },}

```

The expiration (or rather Max Age) of the optimized image is defined by either the `minimumCacheTTL` or the upstream image `Cache-Control` header, whichever is larger.

If you need to change the caching behavior per image, you can configure [`headers`](https://nextjs.org/docs/app/api-reference/next-config-js/headers) to set the `Cache-Control` header on the upstream image (e.g. `/some-asset.jpg`, not `/_next/image` itself).

There is no mechanism to invalidate the cache at this time, so its best to keep `minimumCacheTTL` low. Otherwise you may need to manually change the [`src`](https://nextjs.org/docs/app/api-reference/components/image#src) prop or delete `<distDir>/cache/images`.

### [`disableStaticImages`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#disablestaticimages)

The default behavior allows you to import static files such as `import icon from './icon.png'` and then pass that to the `src` property.

In some cases, you may wish to disable this feature if it conflicts with other plugins that expect the import to behave differently.

You can disable static image imports inside your `next.config.js`:

```js
module.exports = { images: { disableStaticImages: true, },}

```

### [`dangerouslyAllowSVG`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#dangerouslyallowsvg)

The default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) does not optimize SVG images for a few reasons. First, SVG is a vector format meaning it can be resized losslessly. Second, SVG has many of the same features as HTML/CSS, which can lead to vulnerabilities without proper [Content Security Policy (CSP) headers](https://nextjs.org/docs/app/api-reference/next-config-js/headers#content-security-policy).

Therefore, we recommended using the [`unoptimized`](https://nextjs.org/docs/app/api-reference/components/image#unoptimized) prop when the [`src`](https://nextjs.org/docs/app/api-reference/components/image#src) prop is known to be SVG. This happens automatically when `src` ends with `".svg"`.

However, if you need to serve SVG images with the default Image Optimization API, you can set `dangerouslyAllowSVG` inside your `next.config.js`:

```js
module.exports = { images: { dangerouslyAllowSVG: true, contentDispositionType: 'attachment', contentSecurityPolicy: "default-src 'self'; script-src 'none'; sandbox;", },}

```

In addition, it is strongly recommended to also set `contentDispositionType` to force the browser to download the image, as well as `contentSecurityPolicy` to prevent scripts embedded in the image from executing.

### [`contentDispositionType`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#contentdispositiontype)

The default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) sets the [`Content-Disposition`<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition#as_a_response_header_for_the_main_body) header to `attachment` for added protection since the API can serve arbitrary remote images.

The default value is `attachment` which forces the browser to download the image when visiting directly. This is particularly important when [`dangerouslyAllowSVG`](https://nextjs.org/docs/app/api-reference/components/image#dangerouslyallowsvg) is true.

You can optionally configure `inline` to allow the browser to render the image when visiting directly, without downloading it.

```js
module.exports = { images: { contentDispositionType: 'inline', },}

```

## [Animated Images<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#animated-images)

The default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) will automatically bypass Image Optimization for animated images and serve the image as-is.

Auto-detection for animated files is best-effort and supports GIF, APNG, and WebP. If you want to explicitly bypass Image Optimization for a given animated image, use the [unoptimized](https://nextjs.org/docs/app/api-reference/components/image#unoptimized) prop.

## [Responsive Images<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#responsive-images)

The default generated `srcset` contains `1x` and `2x` images in order to support different device pixel ratios. However, you may wish to render a responsive image that stretches with the viewport. In that case, you'll need to set [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) as well as `style` (or `className`).

You can render a responsive image using one of the following methods below.

### [Responsive image using a static import<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#responsive-image-using-a-static-import)

If the source image is not dynamic, you can statically import to create a responsive image:

```js
//components/author.js

import Image from 'next/image'import me from '../photos/me.jpg' export default function Author() { return ( <Image src={me} alt="Picture of the author" sizes="100vw" style={{ width: '100%', height: 'auto', }} /> )}

```

Try it out:

- [Demo the image responsive to viewport<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/responsive)

### [Responsive image with aspect ratio<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#responsive-image-with-aspect-ratio)

If the source image is a dynamic or a remote url, you will also need to provide `width` and `height` to set the correct aspect ratio of the responsive image:


```js
//components/page.js

import Image from 'next/image' export default function Page({ photoUrl }) { return ( <Image src={photoUrl} alt="Picture of the author" sizes="100vw" style={{ width: '100%', height: 'auto', }} width={500} height={300} /> )}

```

Try it out:

- [Demo the image responsive to viewport<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/responsive)

### [Responsive image with `fill`<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#responsive-image-with-fill)

If you don't know the aspect ratio, you will need to set the [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) prop and set `position: relative` on the parent. Optionally, you can set `object-fit` style depending on the desired stretch vs crop behavior:

```js
import Image from 'next/image' export default function Page({ photoUrl }) { return ( <div style={{ position: 'relative', width: '300px', height: '500px' }}> <Image src={photoUrl} alt="Picture of the author" sizes="300px" fill style={{ objectFit: 'contain', }} /> </div> )}

```

Try it out:

- [Demo the `fill` prop<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/fill)

## [Theme Detection CSS<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#theme-detection-css)

If you want to display a different image for light and dark mode, you can create a new component that wraps two `<Image>` components and reveals the correct one based on a CSS media query.

```js
//components/theme-image.module.css

.imgDark { display: none;} @media (prefers-color-scheme: dark) { .imgLight { display: none; } .imgDark { display: unset; }}

<svg fill="none" height="14" viewbox="0 0 512 512" width="14" xmlns="http://www.w3.org/2000/svg"><rect fill="currentColor" height="512" rx="50" width="512"></rect><rect fill="currentColor" height="512" rx="50" width="512"></rect><path clip-rule="evenodd" d="m316.939 407.424v50.061c8.138 4.172 17.763 7.3 28.875 9.386s22.823 3.129 35.135 3.129c11.999 0 23.397-1.147 34.196-3.442 10.799-2.294 20.268-6.075 28.406-11.342 8.138-5.266 14.581-12.15 19.328-20.65s7.121-19.007 7.121-31.522c0-9.074-1.356-17.026-4.069-23.857s-6.625-12.906-11.738-18.225c-5.112-5.319-11.242-10.091-18.389-14.315s-15.207-8.213-24.18-11.967c-6.573-2.712-12.468-5.345-17.685-7.9-5.217-2.556-9.651-5.163-13.303-7.822-3.652-2.66-6.469-5.476-8.451-8.448-1.982-2.973-2.974-6.336-2.974-10.091 0-3.441.887-6.544 2.661-9.308s4.278-5.136 7.512-7.118c3.235-1.981 7.199-3.52 11.894-4.615 4.696-1.095 9.912-1.642 15.651-1.642 4.173 0 8.581.313 13.224.938 4.643.626 9.312 1.591 14.008 2.894 4.695 1.304 9.259 2.947 13.694 4.928 4.434 1.982 8.529 4.276 12.285 6.884v-46.776c-7.616-2.92-15.937-5.084-24.962-6.492s-19.381-2.112-31.066-2.112c-11.895 0-23.163 1.278-33.805 3.833s-20.006 6.544-28.093 11.967c-8.086 5.424-14.476 12.333-19.171 20.729-4.695 8.395-7.043 18.433-7.043 30.114 0 14.914 4.304 27.638 12.912 38.172 8.607 10.533 21.675 19.45 39.204 26.751 6.886 2.816 13.303 5.579 19.25 8.291s11.086 5.528 15.415 8.448c4.33 2.92 7.747 6.101 10.252 9.543 2.504 3.441 3.756 7.352 3.756 11.733 0 3.233-.783 6.231-2.348 8.995s-3.939 5.162-7.121 7.196-7.147 3.624-11.894 4.771c-4.748 1.148-10.303 1.721-16.668 1.721-10.851 0-21.597-1.903-32.24-5.71-10.642-3.806-20.502-9.516-29.579-17.13zm-84.159-123.342h64.22v-41.082h-179v41.082h63.906v182.918h50.874z" fill="var(--ds-background-100)" fill-rule="evenodd"></path></svg>
components/theme-image.tsx

```

```TypeScript
import styles from './theme-image.module.css'import Image, { ImageProps } from 'next/image' type Props = Omit<ImageProps, 'src' | 'priority' | 'loading'> & { srcLight: string srcDark: string} const ThemeImage = (props: Props) => { const { srcLight, srcDark, ...rest } = props  return ( <> <Image {...rest} src={srcLight} className={styles.imgLight} /> <Image {...rest} src={srcDark} className={styles.imgDark} /> </> )}

```

> 
> **Good to know**: The default behavior of `loading="lazy"` ensures that only the correct image is loaded. You cannot use `priority` or `loading="eager"` because that would cause both images to load. Instead, you can use [`fetchPriority="high"`<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/API/HTMLImageElement/fetchPriority).

Try it out:

- [Demo light/dark mode theme detection<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://image-component.nextjs.gallery/theme)

## [getImageProps<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#getimageprops)

For more advanced use cases, you can call `getImageProps()` to get the props that would be passed to the underlying `<img>` element, and instead pass to them to another component, style, canvas, etc.

This also avoid calling React `useState()` so it can lead to better performance, but it cannot be used with the [`placeholder`](https://nextjs.org/docs/app/api-reference/components/image#placeholder) prop because the placeholder will never be removed.

### [Theme Detection Picture<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#theme-detection-picture)

If you want to display a different image for light and dark mode, you can use the [`<picture>`<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/docs/Web/HTML/Element/picture) element to display a different image based on the user's [preferred color scheme<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme).

```ts
import { getImageProps } from 'next/image' export default function Page() { const common = { alt: 'Theme Example', width: 800, height: 400 } const { props: { srcSet: dark }, } = getImageProps({ ...common, src: '/dark.png' }) const { props: { srcSet: light, ...rest }, } = getImageProps({ ...common, src: '/light.png' })  return ( <picture> <source media="(prefers-color-scheme: dark)" srcSet={dark} /> <source media="(prefers-color-scheme: light)" srcSet={light} /> <img {...rest} /> </picture> )}

```

### [Art Direction<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#art-direction)

If you want to display a different image for mobile and desktop, sometimes called [Art Direction<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images#art_direction), you can provide different `src`, `width`, `height`, and `quality` props to `getImageProps()`.

```ts
import { getImageProps } from 'next/image' export default function Home() { const common = { alt: 'Art Direction Example', sizes: '100vw' } const { props: { srcSet: desktop }, } = getImageProps({ ...common, width: 1440, height: 875, quality: 80, src: '/desktop.jpg', }) const { props: { srcSet: mobile, ...rest }, } = getImageProps({ ...common, width: 750, height: 1334, quality: 70, src: '/mobile.jpg', })  return ( <picture> <source media="(min-width: 1000px)" srcSet={desktop} /> <source media="(min-width: 500px)" srcSet={mobile} /> <img {...rest} style={{ width: '100%', height: 'auto' }} /> </picture> )}

```

### [Background CSS<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#background-css)

You can even convert the `srcSet` string to the [`image-set()`<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://developer.mozilla.org/en-US/docs/Web/CSS/image/image-set) CSS function to optimize a background image.

```ts
import { getImageProps } from 'next/image' function getBackgroundImage(srcSet = '') { const imageSet = srcSet .split(', ') .map((str) => { const [url, dpi] = str.split(' ') return `url("${url}") ${dpi}` }) .join(', ') return `image-set(${imageSet})`} export default function Home() { const { props: { srcSet }, } = getImageProps({ alt: '', width: 128, height: 128, src: '/img.png' }) const backgroundImage = getBackgroundImage(srcSet) const style = { height: '100vh', width: '100vw', backgroundImage }  return ( <main style={style}> <h1>Hello World</h1> </main> )}

```

## [Known Browser Bugs<svg viewbox="0 0 16 16" height="0.7em" width="0.7em"><g stroke-width="1.2" fill="none" stroke="currentColor"><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M8.995,7.005 L8.995,7.005c1.374,1.374,1.374,3.601,0,4.975l-1.99,1.99c-1.374,1.374-3.601,1.374-4.975,0l0,0c-1.374-1.374-1.374-3.601,0-4.975 l1.748-1.698"></path><path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" d="M7.005,8.995 L7.005,8.995c-1.374-1.374-1.374-3.601,0-4.975l1.99-1.99c1.374-1.374,3.601-1.374,4.975,0l0,0c1.374,1.374,1.374,3.601,0,4.975 l-1.748,1.698"></path></g></svg>](https://nextjs.org/docs/app/api-reference/components/image#known-browser-bugs)

This `next/image` component uses browser native [lazy loading<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://caniuse.com/loading-lazy-attr), which may fallback to eager loading for older browsers before Safari 15.4. When using the blur-up placeholder, older browsers before Safari 12 will fallback to empty placeholder. When using styles with `width`/`height` of `auto`, it is possible to cause [Layout Shift<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://web.dev/cls/) on older browsers before Safari 15 that don't [preserve the aspect ratio<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://caniuse.com/mdn-html_elements_img_aspect_ratio_computed_from_attributes). For more details, see [this MDN video<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://www.youtube.com/watch?v=4-d_SoCHeWE).

- [Safari 15 - 16.3<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://bugs.webkit.org/show_bug.cgi?id=243601) display a gray border while loading. Safari 16.4 [fixed this issue<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://webkit.org/blog/13966/webkit-features-in-safari-16-4/#:~:text=Now%20in%20Safari%2016.4%2C%20a%20gray%20line%20no%20longer%20appears%20to%20mark%20the%20space%20where%20a%20lazy%2Dloaded%20image%20will%20appear%20once%20it%E2%80%99s%20been%20loaded.). Possible solutions:
    - Use CSS `@supports (font: -apple-system-body) and (-webkit-appearance: none) { img[loading="lazy"] { clip-path: inset(0.6px) } }`
    - Use [`priority`](https://nextjs.org/docs/app/api-reference/components/image#priority) if the image is above the fold
- [Firefox 67+<svg class="with-icon_icon__MHUeb" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewbox="0 0 24 24" width="24"><path d="M7 17L17 7"></path><path d="M7 7h10v10"></path></svg>](https://bugzilla.mozilla.org/show_bug.cgi?id=1556156) displays a white background while loading. Possible solutions:
    - Enable [AVIF `formats`](https://nextjs.org/docs/app/api-reference/components/image#formats)
    - Use [`placeholder`](https://nextjs.org/docs/app/api-reference/components/image#placeholder)