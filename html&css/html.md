# Text
Element | Description | Browser behaviour
--- | --- | --
`<b>` | represents a section of the text that would be presented in a visually different way (for examble key words in a paragraph) although the use of this element does not imply any additional meaning | characters appear bold.
`<i>` | also represents a section of the text that would be said in a different way from surrounding content - such as technical terms, names of ships, foreign words, toughts, or other terms that would usually be italicized | characters appear italic
`<sup>` | superscript
`<sub>` | subscript

## Semantic Markup
Element | Description | Browser behaviour
--- | --- | ---
`<strong>` | indicates that its content has strong importance. For example, the words contained in this element might be said with strong emphasis | characters in bold
`<em>` | indicates emphasis that subtly changes the meaning of a sentence | characters in italic
`<blockquote>` | used for longer quotes that take up an entire paragraph | content indent
`<q>` | used for shorter quotes that sit within a paragraph | add quotes
| | Both `blockquote` and `q` elements may use the `cite` attribute to indicate where the quote is from. It's value should be a URL.
`<abbr>` | can be used if you use an abbreviation or an acronym. A `title` attribute is used to specify the full term.
`<cite>` | can be used when referencing a piece of work such as a book, film or research paper | characters in italics
`<dfn>` | used to inticate the defining instance of a new term (the first time you explain some new terminology in a document | may show in italics
`<mark>` | represents text which is marked or highlighted, due to the marked passage's relevance or importance in the enclosing context | highlighted background
`<ins>` and `<del>` | `<ins>` can be used to show content that has been inserted into a document, while `<del>` element can show text that has been deleted from it. | `<ins>` underline ; `<del>` line through it
`<address>` | used to contain contact details for the author of the page. It can contain a physical address, phone number or email address | content in italics
`<time>` | along with the datetime attribute is used to standardize times. A  valid format of a date is held by the `datetime` attribute. This is the value accessed by assistive devices

# Lists
Element | Description
--- | ---
`<ol>` | ordered list
`<ul>` | unordered list
`<li>` | list item
`<dl>` | definition list. Consists of a series of terms and their definitions. Inside it, you usually see pairs of `<dt>` and `<dd>` elements.
`<dt>` | contain the term being defined (the definition term)
`<dd>` | contain the definition

# Images
### `<img>` Attributes
__`url`__ → link to the image.\
__`alt`__ → provides a text description of the image which describes the image if the user cannot see it.\
__`title`__ → provide additional information about the image. Most browsers will display the content of this attribute in a tooltip when the user hovers over the image.

### `<figure>`
Element that contains images and their caption, so that the two are associated. You can have more than one image inside the `<figure>` element as long as they all share the same caption.\
To add a caption to an image, we use the `<figcaption>` tag.

# Forms
### Form Structure
__`action`__ → URL for the page on the server that will receive the information in the form when it is submitted.\
__`method`__ -> HTTP method to be used to send the form. The most commons are GET or POST.

__`name`__ → used on the form elements. Identifies the form control and is send along with the information to the server.\
__`maxlength`__ & __`minlength`__ → limit the number of characters a user may enter into a field.\
__`placeholder`__ → value is text that will be shown in the text box until the user clicks in that area.

### Text input
`<input type="...">`
- `"text"` → single-line text input.
- `"password"` -> text box that acts just like a single-line text input, except the characters are blocked out.
- `"date"`
- `"email"`
- `"url"`
- `"search"`

### Text Area
Used to create a multi-line text input. It is not an empty element. Any text that appears between the opening `<textarea>` and closing `</textarea>` tags will appear in the text box when the page loads.

### Radio Button & Checkbox
`<input type="...">`
- `"radio"` → allows users to pick just one of a number of options. Once a radio button is selected, it cannot be deselected.
- `"checkbox"` → allows users to select (and unselect) one or more options to answer to a question.
#### Values
`checked` → can be used to indicate which value (if any) shoud be selected when the page loads. The value of this attribute is checked.\
`value` → indicates the value that is sent to the server for the selected option.

### Dropdown List Box & Multiple Select Box
`<select>` → allows users to select one option from a dropdown list. It contains two or more `<option>` elements.
- `size` -> turn a drop down select box into a box that shows more that one option. Its value should be the number of options we want to show at once.
- `multiple` -> allow users to select multiple options from this list.

`<option>` → used to specify the options that the user can select from.
- `selected` → can be used to indicate the option that should be selected when the page loads. The value of this attribute is selected. If this attribute is not used, the first option will be shown when the page loads.

### File Input Box
`<input type="...">`
- `"file"` → creates a box that looks like a text input followed by a browse button. When the user clicks on the browse button, a window opens up that allows them to select a file from  their  computer to be uploaded to the website.

### Submit Button
`<input type="...">`
- `"submit"` → sends the form to the server.
- `"image"` → use an image for the submit button.

`<button>` → was introduced to allow users more control over now their buttons appear, and to allow other elements to appear inside the button. The default `type` is submit.

### Hidden Controls
`<input type="...">`
- `"hidden"` → is not shown on the page. They allow web page authors to add values to forms that users cannot see. For example, a web page author might use a hidden field to indicate which page the user was on when they submitted a form.

### Grouping Form Elements
`<fieldset>` -> group related form controls together. Most browsers will show the fieldset with a line around te edge to show how they are related.
`<legend>` -> contains a caption which helps identify the purpose of that group of form controls.

# `<meta>`
`<meta>` -> lives inside the `<head>` element and contains information about that webpage.

The most common attributes are the **name** and **content** attributes, which tend to be used together. These attributes specify properties of the entire page. The  value of the name attribute is the property you are setting, and the value of the content attribute is the  value that you want to give to this property.

Some defined values for this attribute that are commonly used are:
- `description` -> contains a description of the page. This description is commonly used by search engines to understand what the page is about and should be a maximum of 155 characters. Sometimes it is also displayed in search engines results.
- `keywords` -> contains a list of comma-separated words that a user might search on to find the page.
- `robots` -> indicates whether search engines should add this page to their search results or not. A value of `noindex` can be used if this page should not be added. A value of `nofollow` can be used if search engines should add his page in their results but not any pages that it links to.

The `<meta>` element also uses the **http-equiv** and **content** attributes in pairs.
- `author` -> defines the author of the web page.
- `pragma` -> prevents the browser from caching the page.
- `expires` -> because browsers often cache the content of a page, the expires option can be used to indicate when the page should expire.

# HTML5 tags
Tag | Description
--- | ---
`<header>` | used for the main header at the top of every page, or of an `<article>` or `<section>` within that page.
`<footer>` | used for the main footer at the bottom of every page, or of an `<acticle>` or `<section>` within that page.
`<nav>` | used to contain the major navigational blocks on the site such as the primary site navigation.
`<article>` | acts as a container for any section of a page that could stand alone and potentially be syndicated. This could be an individual article or blog entry, a comment or forum post, or any other independent piece of content.
`<aside>` | It has two purposes: if it's inside an `<article>` element, it should contain information that is related to the article but not essential to its overall meaning. When outside of it, it acts like content that is related to the entire page.
`<section>` | groups related content together, and typically each section would have its own heading. Because the `<section>` element groups related items together, it may contain several distinct `<article>` elements that have a common theme or purpose.
`<hgroup>` | groups together a set of one or more `<h1>` through `<h6>` elements so that they are treated as one single heading.
`<figure>` | it can be used to contain any content that is referenced from the main flow of an article (not just images). The article should still make sense if te content of the `<figure>` were moved. *e.g.*: images, videos, graphs, diagrams, code samples and text that supports the main body of an article.

## HTML5 To Older Browsers
The HTML5 Shiv enables use of HTML5 sectioning elements in legacy Internet Explorer and provides basic HTML5 styling for Internet Explorer 6-9, Safari 4.x (and iPhone 3.x), and Firefox 3.x..

It should be placed inside a conditional comment which checks if the browser version is less than (hence the `lt`) IE9.
```html
<!--[if lt IE 9]>
<script src="https://raw.githubusercontent.com/aFarkas/html5shiv/master/src/html5shiv.js"></script>
<![endif]-->
```

To the CSS add:
```css
header, section, footer, aside, nav, article, figure {
  display: block;
}
```

# Audio
HTML5's audio element gives semantic meaning when it wraps wound or audio stream content in your markup. Audio content also needs a text alternative to be accessible to people who are deaf or hard of hearing. This can be done with nearby text on the page or a link to a transcript.
- `controls` -> shows the browser default play, pause and other controls, and supports keyboard functionality. It's a boolean attribute.

*e.g.*
```html
<audio id="meowClip" controls>
  <source src="audio/meow.mp3" type="audio/mpeg" />
  <source src="audio/meow.ogg" type="audio/ogg" />
</audio>
```

# Accessibility
When information is in a visual format (like a chart), screen reader users need an alternative presentation (like a table) to access the data. An example of the CSS rules that accomplish this:

```css
.sr-only {
  position: absolute;
  left: -10000px;
  width: 1px;
  height: 1px;
  top: auto;
  overflow: hidden;
}
```
- **Note:** `display: none` or `visibility: hidden` hides content for everyone, including screen reader users, and zero values for pixel sizes (such as `width: 0px`) removes that element from the flow of your document, meaning screen readers will ignore it.

### `accesskey` attribute
Used to specified a shortcut key to activate or bring focus to an element. HTML5 allows this attribute to be used on any element, but it's particularly useful when it's used with interactive ones (links, buttons, form controls, etc.)
```html
<button accesskey="b">Important Button</button>
```

### `tabindex` attribute
It indicates that element can be focused on and the value (an integer +, - or 0) determines the behavior. A negative value indicates that an element is focusable, but is not reachable by the keyboard. Adding this attribute on p, span and divs also enables the CSS pseudo-class `:focus`.

It can also specify the exact tab order of elements. This is achieved when the value of the attribute is set to a positive number of 1 or higher. This also will bring keyboard focus to that element first. Then it cycles through the sequence of specified tabindex values, before moving to default and `tabindex="0"` items.

# Sources
HTML & CSS Design and Build Websites, *Jon Duckett*\
[freeCodeCamp](https://freecodecamp.org)