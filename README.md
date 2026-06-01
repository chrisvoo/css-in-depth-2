# CSS in Depth, 2nd edition

Code listings from [CSS In Depth, second edition](https://www.manning.com/books/css-in-depth-second-edition?a_aid=kjg&a_bid=a7bc24da) by Keith J. Grant

```css
/* ruleset */
/* selector -> */ body {   /* declaration block */
  color: black;  /* <- declaration */
  font-family: Helvetica;
  font: font: 32px Helvetica, Arial, sans-serif; /* shorthand property */
}
```

- [CSS in Depth, 2nd edition](#css-in-depth-2nd-edition)
  - [Cascade, specificity, and inheritance](#cascade-specificity-and-inheritance)
    - [Special values](#special-values)
    - [Feature queries using @supports()](#feature-queries-using-supports)
  - [Working with relative units](#working-with-relative-units)
- [Resources](#resources)



##  Cascade, specificity, and inheritance

When declarations conflict, the cascade considers six criteria in the following order to resolve the difference:

1. <b>Stylesheet origin</b>: author styles vs user agent's default styles vs user styles (customizations added by the end user). Declarations marked !important are treated as a higher-priority origin. The overall order of preference, in decreasing order, is as follows:
   1. Important user-agent
   2. Important user
   3. Important author
   4. Normal author
   5. Normal user
   6. Normal user-agent
2. <b>Inline styles</b>: declaration is applied to an element via the HTML style attribute or a CSS selector. If the inline styles are marked as important, then nothing can override them
3. <b>Layer styles</b>: defined in layers, each with a different priority.
4. <b>Selector specificity</b>: selectors precedence, can be indicated with form `X.Y.Z`, where X is the number of IDs, Y the number of classes and Z the number of tags. Pseudo-class selectors (for example, `:hover`) and attribute selectors (for example, `[type="input"]`) each have the same specificity as a class selector. The universal selector (*) and combinators (>, +, ~) have no effect on specificity. See appendix A for more on these types of selectors. The exact rules of specificity are
    1. If a selector has more IDs, it wins
    2. If that results in a tie, the selector with the most classes wins.
    3. If that results in a tie, the selector with the most tag names wins.
1. <b>Scope proximity</b>: whether the styles are scoped to a portion of the DOM.
2. <b>Source order</b>: order in which styles are declared in the stylesheet. If you make the two conflicting selectors equal in specificity, then whichever appears last wins.


> [!NOTE]
> A **cascaded value** is a value for a particular property applied to an element as a result of the cascade. If an element has no cascaded value for a given property, it may **inherit** one from an ancestor element.
> Not all properties are inherited, primarily properties pertaining to text and lists.

### Special values

There are some special values that you can apply to any property to help manipulate the cascade: inherit, initial, unset, and revert.

* `inherit`: it will cause the element to inherit that value from its parent
* `initial`: every CSS property has an initial, or default, value. If you assign the value initial to that property, then it effectively resets to its default value. It's like a hard reset of that value.
* `unset`: when applied to an inherited property, it sets the value to inherit, and when applied to a noninherited property, it sets the value to initial.
* `revert`: override your previously set author styles but leave the user-agent styles intact

> [!NOTE]
> These keywords are normal cascaded values. That means it is still possible to override them with other values when another selector with higher specificity targets the same element.

### Feature queries using @supports()

You can use a feature query to provide a larger set of styles depending on whether or not the browser supports a given feature.

```css
@supports (display: grid) { ... }
```

If the browser understands the declaration (in this case, it supports grid), it applies any rulesets that appear between the braces. If it doesn't understand this, it will ignore them.
Feature queries may be constructed in a few other ways as well:

* `@supports not(<declaration>)`: Only apply rules in the feature query block if the queried declaration isn't supported.
* `@supports (<declaration>) or (<declaration>)`: apply rules if either queried declaration is supported.
* `@supports (<declaration>) and (<declaration>)`: Apply rules only if both queried declarations are supported.
* `@supports selector(<selector>)`: apply rules only if the given selector is understood by the browser (for example, @supports selector(:user-invalid)).

## Working with relative units

Length is the formal name for a CSS value that denotes a distance measurement. It's a number followed by a unit, such as 5px. Percentages are similar to lengths, but strictly speaking, they're not considered lengths.

* **pixels**: type of absolute unit. 1 in. = 25.4 mm = 101.6 Q = 2.54 cm = 6 pc = 72 pt = 96 px
* **em**: relative unit: 1 em means the font size of the current element; its exact value varies depending on the element you're applying it to. `font-size` ems are derived from the inherited font size.
* **rem**: short for "root em". Instead of being relative to the current element, rems are relative to the root element.

> [!NOTE]
> If you know the pixel-based font size you'd like but want to specify the declaration in ems, here's a simple formula: divide the desired pixel size by the parent (inherited) pixel size. For example, if you want a 10 px font and your element is inheriting a 12 px font, 10 / 12 = 0.8333 em.

👉 When in doubt, use rems for font size, pixels for borders, and either ems or rems for most other properties.

# Resources

* https://caniuse.com
* https://developer.mozilla.org/en-US/docs/Web/CSS