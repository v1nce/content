---
title: '-webkit-box-reflect'
slug: Web/CSS/-webkit-box-reflect
tags:
  - '-webkit-box-reflect'
  - CSS
  - CSS Property
  - CSS:WebKit Extensions
  - Non-standard
  - Reference
  - recipe:css-property
browser-compat: css.properties.-webkit-box-reflect
---

{{CSSRef}}{{Non-standard_Header}}

The **`-webkit-box-reflect`** [CSS](/en-US/docs/Web/CSS) property lets you reflect the content of an element in one specific direction.

```css
/* Direction values */
-webkit-box-reflect: above;
-webkit-box-reflect: below;
-webkit-box-reflect: left;
-webkit-box-reflect: right;

/* Offset value */
-webkit-box-reflect: below 10px;

/* Mask value */
-webkit-box-reflect: below 0 linear-gradient(transparent, white);

/* Global values */
-webkit-box-reflect: inherit;
-webkit-box-reflect: initial;
-webkit-box-reflect: unset;
```

> **Warning:** This feature is **not intended to be used by Web sites**. To achieve reflection on the Web, the standard way is to use the CSS {{CSSxRef("element", "element()")}} function.

## Syntax

### Values

- `above`_,_ `below`_,_ `right`_,_ `left`
  - : Are keywords indicating in which direction the reflection is to happen.
- {{CSSxRef("&lt;length&gt;")}}
  - : Indicates the size of the reflection.
- {{CSSxRef("&lt;image&gt;")}}
  - : Describes the mask to be applied to the reflection.

## Formal definition

{{CSSInfo}}

## Formal syntax

```plain
-webkit-box-reflect =
  [ above | below | right | left ]? <length>? <image>?
```

## Specifications

Not part of any standard. The standard way to do reflection in CSS is to use the CSS {{CSSxRef("element", "element()")}} function.

## Browser compatibility

{{Compat}}

## Firefox Polyfill

You can use the following polyfill for firefox.
The polyfill has severe limitations : 
 it can't be used directly on image ; you'll need a container.
 you'll need to tweak it for every image. So it's not very convenient. 

You'll need to add the following static css

```css
.reflection-box
{
 display:inline-block;
 position:relative;
}
You can use 
.reflection-box:after
{
 z-index:10;
 content:"";
 position:absolute;
 width:100%;
 height:100%; 
}

.reflection-box.reflection-above:after
{
 left:0;
 top:calc(var(--offset) * -1); 
 transform-origin: top ;
 transform:scaleY(-1);
}

.reflection-box.reflection-below:after
{
 left:0;
 top:var(--offset);
 transform-origin: bottom ;
 transform:scaleY(-1);
}

.reflection-box.reflection-left:after
{
 top:0;
 left:calc(var(--offset) * -1);  
 transform-origin: left ;
 transform:scaleX(-1);
}
 
.reflection-box.reflection-right:after
{
 top:0;
 left:var(--offset);
 transform-origin: right ;
 transform:scaleX(-1);
}
```

The image needs to be wrapped inside a container with a class "reflection-box".

```plain
<span class="reflection-box">
 <img src="imageToReflect.jpg" alt="...">
</span>
```

Depending on the side of the reflection, you should add an additional class : "reflection-above", "reflection-below", "reflection-left", "reflection-right".

You should define a variable --offset on the container.
If all your reflections will have the same offset, you could define it on the class "reflection-box"

```css
.reflection-box
{
 --offset:10px;
}

```

Then, you'll need to define the reflection image.
You'll probably want a distinct image per reflection, so I suggest you use an id both for the image to be reflected and for its container.

```plain
<span id="reflexion1" class="reflection-box reflection-right">
 <img id="reflexion1img" src="imageToReflect.jpg" alt="...">
</span>
```

You should use -moz-element to duplicate the image as a reflection.

```css
#reflection1:after
{
 background: -moz-element(#reflexion1img) no-repeat;
}

```

The final touch will be to add the image mask.

```css
#reflection1:after
{
 mask-image: linear-gradient(rgba(0, 0, 0, 1.0) 50%, transparent 100%); 
}

```

## See also

- The Apple [documentation](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html).
- The Webkit [specification](https://webkit.org/blog/182/css-reflections/).
- Lea Verou's article on reflection using [CSS features on the standard track](https://lea.verou.me/2011/06/css-reflections-for-firefox-with-moz-element-and-svg-masks/).
