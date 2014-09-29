# HTML & Template

> **TEAM**: This document is taken from Github. Please use or remove it.

## Markup & Styles

### Doctype

A proper doctype which triggers standards mode in your browser should always be used. Quirks mode should always be avoided.

For simplicity, we use the html5 doctype:

```html
<!DOCTYPE html>
```

### Coding style

#### General formatting

- Paragraphs of text should always be placed in a `<p>` tag. Never use multiple `<br>` tags.
- Items in list form should always be in `<ul>`, `<ol>`, or `<dl>`. Never use a set of `<div>` or `<p>`.
- Every form input that has text attached should utilize a <label> tag. Especially radio or checkbox elements.
- Even though quotes around attributes is optional, always put quotes around attributes for readability.
- Avoid writing closing tag comments, like `<!-- /.element -->`. This just adds to page load time. Plus, most editors have indentation guides and open-close tag highlighting.
- Avoid trailing slashes in self-closing elements. For example, `<br>`, `<hr>`, `<img>`, and `<input>`.
- Don't set tabindex manually—rely on the browser to set the order.

