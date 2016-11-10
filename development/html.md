#HTML

##Best practices

###Avoid id attributes
The use of id attributes is discouraged when writing HTML. We consider the id attribute to be too generic for any semantic meaning, and  should be used only when conforming to accessibility requirements or using an anchor link. Targeting id attributes with CSS is forbidden as the specificity is too high to be overridden by CSS classes.

####Rationale
* id attributes do not have any semantic meaning, therefore it can be difficult to determine if and how they are being used
* id attributes are overly specific when targeted by CSS
* The same id attribute can only appear once on a page, which may be a challenge when working with components

####Exceptions
* Accessible label for form field input
* Anchor link

####Example
Given the following markup can you be assured that the navbar id is not being targeted by CSS, Javascript, or automation scripts? If you change the id, will anything break?

```html
<div id="navbar"></div>
```

To separate our concerns and give a clearer picture to other developers we would instead suggest:

```html
<div class="navbar js-navbar" data-automation-id="navbar"></div>
```

This gives us confidence that
* `navbar` is a CSS class
* `js-navbar` is a JavaScript binding
* `data-automation-id` is an automation id

Using this approach instead of an id attribute gives us a separation of concerns which allows the CSS class, JavaScript binding, and automation id to change independently of each other.
