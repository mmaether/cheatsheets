# Accessibility Cheat Sheet

Accessibility is the design of software for people who experience disabilities. CypherWorx wants to ensure that disabilities don't hinder an individual from using the site in any capacity, and as such we develop code to help people with disabilities so they can use the site. There are a wide variety of disabilities that we design to help, including: 

- **Visual**: Visual impairments including blindness, various common types of low vision and poor eyesight, various types of color blindness;
- **Motor/mobility**: e.g. difficulty or inability to use the hands, including tremors, muscle slowness, loss of fine muscle control, etc., due to conditions such as Parkinson's Disease, muscular dystrophy, cerebral palsy, stroke;
- **Auditory**: Deafness or hearing impairments, including individuals who are hard of hearing;
- **Seizures**: Photo epileptic seizures caused by visual strobe or flashing effects.
- **Cognitive/Intellectual**: Developmental disabilities, learning disabilities (dyslexia, dyscalculia, etc.), and cognitive disabilities of various origins, affecting memory, attention, developmental "maturity," problem-solving and logic skills, etc.

Web accessibility should be baked-in rather than retrofitted, and all software pushed to live will need to pass our accessibility checks.

For more information please read [WebAim](https://webaim.org/) in its entirety and Wikipedia's article on [web accessibility](https://en.wikipedia.org/wiki/Web_accessibility). See also the [Accessibility Cheatsheet](https://moritzgiessmann.de/accessibility-cheatsheet/).

## Making software accessible ##

1. If there is a native HTML element for something then use it.

      a. Use `<button>` or `<a>` (the former if it triggers an action, the latter if it triggers page navigation) so that a keyboard user can tab to anything they may need to interact with. Avoid adding tabindex="0" to make something tabbable.

      b.Use `<dialog>` for dialogs, `<progress>` for progress bars, `<footer>` for footers.

      c. Use the new HTML form input types.

2. Consult [html5accessibility.com](https://www.html5accessibility.com/) and add the `role` attribute on any element that does not have complete browser support.

3. Markup any status/alert/log as an ARIA live region on page load. Similarly mark up any region that only updates through a DOM attribute (like an image that changes the src and alt) as a live region.

4. Check the [Flesch-Kincaid Readability Score](http://www.thewriter.com/what-we-think/readability-checker/). Aim for a minimum of 60, preferably over 70. Tip: use short sentences and write in a conversational tone. Use the active voice when telling them what to do. For example, the previous sentence started with "Use" and not "You should use".

5. Include headers and make them follow `H1` through `H6`.

6. Have a label for every form input.

7. Check the color contrast of content. Use tools like [contrast-finder.tanaguru.com](http://contrast-finder.tanaguru.com/) or [colorsafe.co](http://colorsafe.co/) to fine tune the content.

8. Zoom the screen to 200% or test with Windows' Magnifier app.

9. For something that should be visually hidden but read to screen readers simply add the Drupal class `element-invisible`. To hide it from everyone add the Drupal class `element-hidden`.

10. If you're creating a widget that does something pretty common to the web (tabs, toolbars, hiding/showing regions, etc.) consult the [OpenAjax Examples](http://oaa-accessibility.org/).

11. Make sure color alone is not used to determine meaning.

12. Use a [color blindness simulator](http://www.color-blindness.com/coblis-color-blindness-simulator/) to check the interface to ensure the correct meaning is conveyed.

13. Install NVDA (and the [focus highlight plugin](http://addons.nvda-project.org/addons/focusHighlight.en.html)) to actually test the interface.

14. Run aXe ([http://bitly.com/aXe-Chrome](http://bitly.com/aXe-Chrome) or [http://bit.ly/aXe-Firefox](http://bit.ly/aXe-Firefox)) to test for issues.

## Standards

There are various accessibility standards that websites need to pass.

- [Section 508](https://www.section508.gov/)
- [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)

It's recommended to complete a [VPAT](https://www.section508.gov/sell/vpat) to meet compliance.

## Accessibility Resources ##

* http://oaa-accessibility.org/
* http://addons.nvda-project.org/addons/focusHighlight.en.html
* http://www.thewriter.com/what-we-think/readability-checker/
* http://contrast-finder.tanaguru.com/
* http://colorsafe.co/
* https://leaverou.github.io/contrast-ratio/
* http://w3c.github.io/aria-in-html/#checklist
* http://www.rgbtohex.net/hextorgb/
* http://w3c.github.io/aria/html-aam/html-aam.html#accessible-name-and-description-calculation
* http://webaim.org/resources/contrastchecker/
* http://tink.uk/using-the-aria-owns-attribute/
* https://thepaciellogroup.github.io/AT-browser-tests/
* https://www.paciellogroup.com/resources/
* http://www.karlgroves.com/2013/05/14/links-are-not-buttons-neither-are-divs-and-spans/
* https://cfpb.github.io/design-manual/best-practices/accessibility-best-practices
* http://www.color-blindness.com/coblis-color-blindness-simulator/
* https://support.microsoft.com/en-us/instantanswers/ece8e1d7-1a7c-473c-a0f4-3c9d66fee295/turn-on-high-contrast-mode
* http://www.weba11y.com/blog/2014/07/07/keyboard-navigation-in-mac-browsers/
* http://heydonworks.com/practical_aria_examples/ - Link is now dead, but the site has other good examples in its archives.
