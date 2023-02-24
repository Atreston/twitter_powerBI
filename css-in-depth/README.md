# CSS in Depth

## CH1

... if you’ve worked with it on any large projects, you know it can grow into unwieldy complexity.

While it’s helpful to know some “tricks” or useful recipes you can follow, mastering CSS requires an understanding of the principles that make those practices possible.

most fundamental principles of the language: the cascade,the box model, and the wide array of unit types available. 

Fundamentally, CSS is about declaring rules: Under various conditions, we want certain things to happen. If this class is added to that element, apply these styles.

When you look at small examples, this process is usually straightforward. But as your stylesheet grows, or the number of pages you apply it to increases, your code can become complex surprisingly quickly. There are often several ways to accomplish the same thing in CSS. A key part of CSS development comes down to writing rules in such a way that they’re predictable.

When declarations conflict, the cascade considers three things to resolve the difference:
1. Stylesheet origin—Where the styles come from. Your styles are applied in conjunction with the browser’s default styles.
2. Selector specificity—Which selectors take precedence over which.
3. Source order—Order in which styles are declared in the stylesheet.

A *declaration* is made up of a property (color) and a value (black):

```css
color: black;
```

A *declaration block* is preceded by a *selector* (in this case, body):

```css
body {
   color: black;
   font-family: Helvetica;
}
```
Together, the selector and declaration block are called a ruleset.

Finally, at-rules are language constructs beginning with an “at” symbol, such as @import rules or @media queries.

There are different types, or origins, of stylesheets. Yours are called author styles; there are also user agent styles, which are the browser’s default styles. 

A number of other things are determined by the **user agent styles**: the list has a left padding and a list-style-type of disc to produce the bullets. Links are blue and underlined. The heading and the list have top and bottom margins.

After user agent styles are considered, the browser applies your styles—the **author styles**.

Overriding user agent styles:

```css
h1 {
   color: #2f4f4f;
   margin-bottom: 10px;
}

#main-nav {
   margin-top: 10px;
   list-style: none;
   padding-left: 0;
}

#main-nav li {
   display: inline-block;
}

#main-nav a {
   color: white;
   background-color: #13a4a4;
   padding: 5px;
   border-radius: 2px;
   text-decoration: none;
}
```

>Check `user-agent-styles.html` and `author-styles.html` running on `https://localhost:3000/` after setting up the `express` server.

A declaration can be marked important by adding !important to the end of the declaration, before the semicolon:

```css
color: red !important;
```

Declarations marked `!important` are treated as a higher-priority origin, so the overall order of preference, in decreasing order, is this:
1. Author important
2. Author
3. User agent

>There are reasons to avoid using ID selectors. More about this in later in this section.

### Understanding specificity

If conflicting declarations can’t be resolved based on their origin, the browser next tries to resolve them by looking at their specificity. Understanding specificity is essential. 

The browser evaluates specificity in two parts: styles applied inline in the HTML and styles applied using a selector.

#### INLINE STYLES

If you use an HTML style attribute to apply styles, the declarations are applied only to that element. These are, in effect, **“scoped” ** declarations, which override any declarations applied from your stylesheet or a `<style>` tag. Inline styles have no selector because they are applied directly to the element they target.

```html
<li>
   <a href="/specials" class="featured" style="background-color: orange;">
      Specials
   </a>
</li>
```

#### SELECTOR SPECIFICITY

The second part of specificity is determined by the selectors. For instance, a selector
with two class names has a higher specificity than a selector with only one. If one declaration sets a background to orange, but another with higher specificity sets it to teal,
the browser applies the teal color.

```css
#main-nav a {
   color: white;
   background-color: #13a4a4;
   padding: 5px;
   border-radius: 2px;
   text-decoration: none;
}

/* This selector won't be applied because the previous ruleset has more SPECIFICITY */
.featured {
   background-color: orange;
}
```

An ID selector has a higher specificity than a class selector, for example. In fact, a single ID has a higher specificity than a selector with any number of classes. Similarly, a class selector has a higher specificity than a tag selector (also called a type selector).

The exact rules of specificity are:
1. If a selector has more IDs, it wins (that is, it’s more specific).
2. If that results in a tie, the selector with the most classes wins.
3. If that results in a tie, the selector with the most tag names wins.

Consider the selectors shown in the following listing:

```css
/* 1 */
html body header h1 {
   color: blue;
}

/* 2 */
body header.page-header h1 {
   color: orange;
}

/* 3 */
.page-header .title {
   color: green;
}
/* 4 */
#page-title {
   color: red;
}
```

The most specific selector here is **4**, with one ID, so its color declaration of red is applied to the title. The next specific is **3**, with two class names. This would be applied if the ID selector **4** were absent. Selector **3** has a higher specificity than selector **2**, despite its length: two classes are more specific than one class. Finally, **1** is the least specific, with four element types (that is, tag names) but no IDs or classes.

> Pseudo-class selectors (for example, `:hover`) and attribute selectors (for example, `[type="input"]`) each have the same specificity as a class selector. The universal selector (*) and combinators (>, +, ~) have no effect on specificity.

#### A notation for specifity

| Selector                   | IDs | Classes | Tags | Notation |
|----------------------------|:---:|:-------:|:----:|:--------:|
| html body header h1        | 0   | 0       | 4    | 0,0,4    |
| body header.page-header h1 | 0   | 1       | 3    | 0,1,3    |
| .page-header .title        | 0   | 2       | 0    | 0,2,0    |
| #page-title                | 1   | 0       | 0    | 1,0,0    |

#### Understanding source order

The third and final step to resolving the cascade is source order. If the origin and the specificity are the same, then the declaration that appears later in the stylesheet—or appears in a stylesheet included later on the page—takes precedence.

This means you can manipulate the source order to style your featured link. If you make the two conflicting selectors equal in specificity, then whichever appears last wins.

```css
.nav a {
   color: white;
   background-color: #13a4a4;
   padding: 5px;
   border-radius: 2px;
   text-decoration: none;
}

/* Same specifity than the previous one (0,1,1) */
/* This ruleset wins due to source order (last wins) */
a.featured { 
   background-color: orange;
}
```

#### Link styles and source order

The cascade is the reason this order matters: given the same specificity, later styles override earlier styles. 

source order affects the cascade. For example, your selectors for styling links should go in a certain order.

This listing shows styles for links on a page in the “correct” order.

```css
a:link {
   color: blue;
   text-decoration: none;
}

a:visited {
   color: purple;
}

a:hover {
   text-decoration: underline;
}

a:active {
   color: red;
}
```

The cascade is the reason this order matters: given the same specificity, later styles override earlier styles. If two or more of these states are true of one element at the same time, the last one can override the others. If the user hovers over a visited link, the hover styles take precedence. If the user activates the link (that is, clicks it) while hovering over it, the active styles take precedence.

#### CASCADED VALUES

The browser follows these three steps — **origin**, **specificity**, and **source order** to resolve every property for every element on the page. A declaration that “wins” the cascade is called a cascaded value.

#### Inheritance

The cascade is frequently conflated with the concept of inheritance. Although the two topics are related, you should understand each individually.

It’s common to apply a font-family to the `<body>` element. All the ancestor elements within will then inherit this font; you don’t have to apply it explicitly to each element on the page.

Not all properties are inherited, however. By default, only certain ones are. In general, these are the properties you’ll want to be inherited. They are primarily properties pertaining to text: `color`, `font`, `font-family`, `font-size`, `font-weight`, `font-variant`, `font-style`, `line-height`, `letter-spacing`, `text-align`, `text-indent`, `text-transform`, `white-space`, and `word-spacing`.

### Special values

There are two special values that you can apply to any property to help manipulate the cascade: `inherit` and `initial`.
