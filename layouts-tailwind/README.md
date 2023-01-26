
## TailwindCSS Dev Configuration

- Add the Play CDN script to your HTML: Add the Play CDN script tag to the `<head>` of your HTML file, and start using Tailwind’s utility classes to style your content.

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```

## HTML Content Sectioning


|               Element              |                                                                                                                                                                                                     Description                                                                                                                                                                                                    |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|` <address>`                          | The `<address>` HTML element indicates that the enclosed HTML provides contact information for a person or people, or for an organization.                                                                                                                                                                                                                                                                           |
| `<article>`                          | The `<article>` HTML  element represents a self-contained composition in a document, page,  application, or site, which is intended to be independently  distributable or reusable (e.g., in syndication). Examples include: a  forum post, a magazine or newspaper article, or a blog entry, a product  card, a user-submitted comment, an interactive widget or gadget, or any  other independent item of content. |
| `<aside>`                            | The `<aside>` HTML  element represents a portion of a document whose content is only  indirectly related to the document's main content. Asides are frequently  presented as sidebars or call-out boxes.                                                                                                                                                                                                             |
| `<footer>`                           | The `<footer>` HTML element represents a footer for its nearest ancestor sectioning content or sectioning root element. A `<footer>` typically contains information about the author of the section, copyright data or links to related documents.                                                                                                                                                                     |
| `<header>`                           | The `<header>` HTML  element represents introductory content, typically a group of  introductory or navigational aids. It may contain some heading elements  but also a logo, a search form, an author name, and other elements.                                                                                                                                                                                     |
|` <h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>` | The `<h1>` to `<h6>` HTML elements represent six levels of section headings. `<h1>` is the highest section level and `<h6>` is the lowest.                                                                                                                                                                                                                                                                                 |
| `<main>`                             | The `<main>` HTML element represents the dominant content of the body  of a document. The main content area consists of content that is  directly related to or expands upon the central topic of a document, or  the central functionality of an application.                                                                                                                                                       |
| `<nav>`                              | The `<nav>` HTML  element represents a section of a page whose purpose is to provide  navigation links, either within the current document or to other  documents. Common examples of navigation sections are menus, tables of  contents, and indexes.                                                                                                                                                               |
| `<section>`                          | The `<section>` HTML  element represents a generic standalone section of a document, which  doesn't have a more specific semantic element to represent it. Sections  should always have a heading, with very few exceptions.                                                                                                                                                                                         |


* [HTML elements reference - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#content_sectioning)

## Using tailwindCSS `container` class

From the docs:

>**Container**
>
>A component for fixing an element's width to the current breakpoint.
>
>_Using the container_
>
>The `container` class sets the `max-width` of an element to match the min-width of the current breakpoint. This is useful if you’d prefer to design for a fixed set of screen sizes instead of trying to accommodate a fully fluid viewport.

* [Container - Tailwind CSS](https://tailwindcss.com/docs/container)

### Example

* [Tailwind CSS Container - GeeksforGeeks](https://www.geeksforgeeks.org/tailwind-css-container/)

_See screenshots folder_

## Adding subRepo

```shell
PS D:\web\vainilla\htmlcss-morgue> git add *
warning: adding embedded git repository: css-testing
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of    
hint: the embedded repository and will not know how to obtain it.        
hint: If you meant to add a submodule, use:
hint: 
hint:   git submodule add <url> css-testing
hint: 
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint: 
hint:   git rm --cached css-testing
hint: 
hint: See "git help submodule" for more information.
PS D:\web\vainilla\htmlcss-morgue> 
```
