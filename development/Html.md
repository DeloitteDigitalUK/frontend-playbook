# HTML

## Best practices

### Avoid id attributes
The use of id attributes is discouraged when writing HTML. We consider the id attribute to be too generic for any semantic meaning, and  should be used only when conforming to accessibility requirements or using an anchor link. Targeting id attributes with CSS is forbidden as the specificity is too high to be overridden by CSS classes.

#### Rationale
* id attributes do not have any semantic meaning, therefore it can be difficult to determine if and how they are being used
* id attributes are overly specific when targeted by CSS
* The same id attribute can only appear once on a page, which may be a challenge when working with components

#### Example
Given the following markup can you be assured that the navbar id is not being targeted by CSS, JavaScript, or automation scripts? If you change the id, will anything break?

```html
<!-- bad -->
<div id="navbar"></div>
```

To separate our concerns and give a clearer picture to other developers we would instead suggest:

```html
<!-- good -->
<div class="navbar js-navbar" data-automation-id="navbar"></div>
```

This gives us confidence that
* `navbar` is a CSS class
* `js-navbar` is a JavaScript binding
* `data-automation-id` is an automation id

Using this approach instead of an id attribute gives us a separation of concerns which allows the CSS class, JavaScript binding, and automation id to change independently of each other.

#### Exceptions
Accessibility spec implementation
```html
<label for="email">Email</label>
<input id="email" name="email" type="email" />
```

Anchor link
```html
<h1 id="site-heading">Our heading</h1>
<a href="#site-heading">Link to heading</a>
```
---
### Use noopener and noreferrer in external links
When your page links to another page using `target="_blank"`, the new page runs on the same process as your page. If the new page is executing expensive JavaScript, your page's performance may also suffer.  

On top of this, `target="_blank"` is also a security vulnerability. The new page has access to your `window` object via `window.opener`, and it can navigate your page to a different URL using `window.opener.location = newURL`.

#### Rationale
* Performance
* Security

#### Example
```html
<!-- bad -->
<a href="https://example.com" target="_blank">...</a>
```
  
```html
<!-- good -->
<a href="https://example.com" target="_blank" rel="noopener">...</a>
```
  
[https://mathiasbynens.github.io/rel-noopener/](https://mathiasbynens.github.io/rel-noopener/)
