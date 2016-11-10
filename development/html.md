#HTML

##Best practices

###Avoid id attributes
The use of id attributes is discouraged when writing HTML. We consider the id attribute to be too generic for any semantic meaning, and only when conforming to accessibility requirements should they be used. Targeting id attributes with CSS is forbidden as the specificity is too high to be overridden by CSS classes.

As an example, given the following markup can you be assured that the navbar id is not being targeted by CSS, Javascript, or automation scripts? If you change the id, will anything break?

```html
<div id="navbar"></div>
```

To seperate our concerns and give a clearer picture to other developers we would instead suggest:

```html
<div class="navbar js-navbar" data-automation-id="navbar"></div>
```

This gives us confidence that
* `navbar` is a CSS class
* `js-navbar` is a JavaScript binding
* `data-automation-id` is an automation id

Using this approach instead of an id attribute gives us a seperation of concerns which allows the CSS class, JavaScript binding, and automation id to change independently of each other.

Exceptions
* Accessible label for form field input
* Ancor link
