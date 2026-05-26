# CSS in Depth, 2nd edition

Code listings from [CSS In Depth, second edition](https://www.manning.com/books/css-in-depth-second-edition?a_aid=kjg&a_bid=a7bc24da) by Keith J. Grant

```css
/* ruleset */
/* selector -> */ body {   /* declaration block */
  color: black;  /* <- declaration */
  font-family: Helvetica;
}
```

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
2. <b>Source order</b>: order in which styles are declared in the stylesheet.