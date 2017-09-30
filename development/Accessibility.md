# Accessibility
## Overview
The W3C have written the WCAG 2.0 Spec related to Accessibility - http://www.w3.org/TR/WCAG/ 
The four principles of accessibility are:
* Perceivable - Available through sight, hearing, or touch.
* Operable - Compatible with keyboard or mouse.
* Understandable - User-friendly, easy to comprehend.
* Robust - Works across browsers, assistive technologies, mobile devices, old devices/browsers, etc.

## Why should we care?
On 8 June 2009 the UK Government ractified the UN Convention on the Rights of Persons with Disabilities. This document states that "access to information, communications and services, including the internet, is a human right." Basically this means, you can be in a lot of trouble if you discriminate against anyone when you have a website with critical information on it (and there is no accessible alternative).
As a starting point, your service should aim to meet Level AA of the Web Content Accessibility Guidelines (WCAG) 2.0.
https://www.gov.uk/service-manual/user-centred-design/accessibility
And it's actually not that hard to achieve it!

## How do you meet WCAG 2.0?
There are 5 key conformance requirements in order to meet WCAG 2.0 compliance (http://www.w3.org/TR/WCAG20/#conformance-reqs)

### Meet the appropriate Conformance Level by following the guidelines outlined in the spec (http://www.w3.org/TR/WCAG/#guidelines) 
* Level A,
* Level AA,
* Level AAA

### Full pages
* Conformance is for full web pages only – you can’t get conformance for only part of the page
* If a single module that appears on a page isn't accessible, the entire page isn't accessible

### Complete processes
* Conformance is for a complete end-to-end process
* If a single step of the process isn't accessible, the entire process isn't accessible

### Only Accessibility-Supported Ways of Using Technologies
* Only accessibility-supported ways of using technology are used to satisfy the success criteria.
* Anything that isn’t supported can successfully pass if you provide an alternative way that is accessibility supported.
* For example - you can give users an accessible PDF document instead of a non-accessible form

### Non-Interference
* If you use a non-accessible way, then don’t block the ability to use the rest of the page.
* Allow accessible users to skip past the non-accessible content

## High Level Checklist
Here is a very high level checklist of things to watch out for. Items in italics are basically best practice HTML, so you should already be doing this

### Level A
* Non-text content (like images) should have text associated
* Audio/Video has transcripts and synchronized captions
    * Valid and Semantic markup is used correctly
    * Tables are used for tabular data only and are marked up with <th> and scope attributes
    * Text labels associated with form fields
* Headings (`<h1>`), lists (`<ul>`, `<ol>`), emphasis (`<em>`, `<strong>`, `<blockquote>`)
* Reading and keyboard navigation order (code order) makes sense
* Instructions don’t rely on shapes/colours/visual-location/sound only
* Colour isn’t the only means of distinguishing visual elements
* All content can be navigated by using a keyboard and you can’t get trapped
* You must be able to stop/pause/mute/adjust volume for automatically playing audio/carousels/animations that last longer than 3 seconds
* No flashes of content more than 3 times per second
* Skip links are included
* Proper page titles
* Proper focus order
* Proper link text (no “Click Here”), links with different endpoints should have different text
* Make sure the site actually behaves as expected
* Include labels and instructions for forms

###Level AA
* Audio description for videos
* Text and images have an appropriate colour contrast ratio
    * Standard Text: 4.5:1
    * Large text (18px or 14px Bold): 3:1
* The page is readable when the text size is doubled
* Don’t use images if it’s just an image of text (even if you use an alt tag)
* Multiple ways are available to find other pages on the site (e.g. list of related pages, table of contents, site map, site search)
* Page headings and labels are informative – no duplicate headings or label text
* Visible keyboard focus state on everything that can be interacted with
* Navigation links that are repeated on pages don’t change order on other pages
* Elements that have the same functionality across the site don’t change
* Include labels and instructions for forms and provide error suggestions and validation help
* If a user can change/delete legal or financial data, the changes/deletions can be reversed, verified or confirmed

###The main points to remember
There really are four main points you need to remember (the rest you should already be doing)
* All content can be navigated by using a keyboard
     * Include skip links to make it a better UX for keyboard only users
* Audio/Video
    * Requires transcripts and synchronized captions (A)
    * Audio description for videos (AA)
* Colours/Design
    * Colour isn’t the only means of distinguishing visual elements (A)
    * Text and images have an appropriate colour contrast ratio (AA)
* Animation
    * You must be able to stop/pause/mute/adjust volume for automatically playing audio/carousels/animations that last longer than 3 seconds (A)
    * No flashes of content more than 3 times per second (A)


## Key areas to focus on
All content can be navigated by using a keyboard

#### How to meet
* Do all the links, buttons and inputs have a :focus state?
* Does the tab order make sense?
* Don’t get stuck in a keyboard trap!
* Include links to skip areas of the page


#### How to test
Using only your keyboard, can you
* Get to everything on the page?
* Use everything that you can with a mouse?
* Can you tab randomly through the page without looking, then figure out where you are in the page as soon as you look?

#### Keyboard traps
There are a couple of ways that you can get trapped using the keyboard only:
* You press tab and instead of the next item, you’re in a completely different part of the page and aren’t sent back
    * AddThis
* You press tab and you end up in an infinite loop through the DOM
    * YouTube’s Flash Player on some browsers
To resolve this, put a Skip Link above, and below the area that has the problem:
```html
<a id="skip-addthis-1-top" href="#skip-addthis-1-bottom" class="vh focusable">Skip below AddThis tool</a>
<!-- AddThis CODE HERE -->
<a id="skip-addthis-1-bottom" href="#skip-addthis-1-top" class="vh focusable">Skip above AddThis tool</a> 
```

### Audio/Video
#### How to meet
* Use a video player that supports captions (e.g. YouTube, Vimeo)
* Work with Design/UX to add a link for Transcripts and Alternative versions of the video if required.
### Using YouTube
If you do use YouTube, here are a couple of tricks to help:
* Use the YouTube iFrame Embed (in Chrome it now uses HTML5 by default)
* Add a “Skip link” before and after the iFrame to avoid keyboard traps
* Add a visuallyhidden link before the iFrame with the YouTube.com link with text: “View [Video Title] on YouTube.com”
    * Encourage the client to put a link back to the Transcript page in the YouTube description

### Colours/Design
#### How to meet
* Work with Design/UX to ensure that links and icons/symbols aren’t only differentiated by colour alone
* Work with the Creative Designer to ensure that text has the appropriate colour contrast ratios
    * Standard Text: 4.5:1
    * Large text (18px or 14px Bold): 3:1
#### How to test
* Use the HTML_CodeSniffer Bookmarklet
    * http://squizlabs.github.io/HTML_CodeSniffer/
* Use a Colour Contract Calculator
    * http://snook.ca/technical/colour_contrast/colour.html

### Animation
#### How to meet
* For all auto playing carousels you must have a play/pause toggle button
* For all auto playing video/audio you must have play/pause/mute/adjust volume buttons
* Don’t cause epileptic episodes! (No flashes of content more than 3 times per second)

#### Even better!
Convince your client to not have auto playing carousels or video/audio!
* The Play/Pause button generally looks ugly
* Auto playing stuff is annoying (especially audio)

## ARIA attributes
### Use ARIA role attributes for landmarks
* ARIA role attributes give additional information and shortcuts to screen readers:
* Add role="button" to significant CTA links (also consider adding JS to allow users to use the Spacebar to activate the link)
* Add role="main" to the main content container
* Add role="navigation" to navigation components like primary and secondary nav
* Add role="complementary" to aside columns of content
* Add role="banner" to the header
* Add role="contentinfo" to footer elements
* Add role="search" to search elements

### Common ARIA attributes
ARIA attributes help explain what’s happening to screen readers, so you don’t have to, some common attributes are:
* aria-hidden: hides the content from a screen reader
* aria-expanded: boolean – explains if the item is expanded or not
* aria-selected: boolean – explains if the item is selected or not
* aria-controls: ID of the item that the link/button effects
* aria-labelledby: ID of the item that describes the current element
* aria-live: Describes an area of the page that is updated by AJAX

### Examples of using ARIA to markup modules
You can find the following examples of where ARIA markup has been used in the Deloitte Middleman Templates.

#### ExpandCollapse module
The JS adds/removes the aria tags as required if the expandcollapse module is enabled/disabled.
* Updated the expandcollapse link
    * Added aria-controls="expanding-id" which points to the content <div>
* Updated the content `<div>`
    * Added role="region"
    * Added aria-expanded="false" that is set to "true" when the content is expanded

#### Tabs module
The JS adds/removes the aria tags as required if the tab module is enabled/disabled.
* Added role="tablist" to the `<ul>` that lists the tabs and role="tab" to the `<li>` for each tab
* Updated the tab link
    * Added an id attribute
    * Added aria-controls="tab-id" which points to the tab content <div>
    * Added aria-selected="false" that is set to "true" when the tab is active (along with some visuallyhidden text that says “Active tab”)
* Updated the tab content <div>
    * Added role="tabpanel"
    * Added aria-labelledby="btn-tab-id" which points to the id on the tab link

#### Simple AJAX updates
This is a very simple example, there are more complex scenarios for aria-live that should be considered in some circumstances
* Add an id, aria-live="polite" and tabindex="-1" to the container that gets updated by AJAX
    * Other possible values for aria-live are off, assertive
* Add aria-controls="container-id" to the links that update the container
* Generally, you could also apply role="region" to the container as well
* When the JS has updated the AJAX, it’s polite to tab the user to the container (by focusing on it)

## Our Role
#### Keeping the BA/UX/Creative team informed
As a FED you are the Accessibility lead on the project.
* Make sure that the PM/Director knows about additional testing time for screen readers/accessibility requirements
* Make sure that the UX guys know that the site should behave as expected
    * UX for screen readers is also important!
* Make sure that the designers know about colour contrast
* Test the project yourself using a screen reader (see below for the different types)

External testing of pages is recommended
* Some clients have their own Accessibility Team

## Quoting
There isn't too much additional work for a standard CMS project:
This is a percentage of the total time required to complete the templates:
* Approx 5-10% for Level A
* Approx 10-20% for Level AA

This includes self testing using a screen reader, running through the accessibility checklist and any fixes for bugs/tweaks.
If you have a complex AJAX situation, or unique UI requirements, consider that you might need more time:
* Approx 20% for multi page AJAX applications
* Approx 20-30% for complex calculators and forms

Also add into your assumptions the WCAG 2.0 level you're meeting and the fact that the templates should be tested for accessibility by the testing team.

## Misc
[Accessibility checklist](http://accessibility.voxmedia.com/)
[W3C on labelling controls](https://www.w3.org/WAI/tutorials/forms/labels/)
[W3C on user notifications](https://www.w3.org/WAI/tutorials/forms/notifications/)
