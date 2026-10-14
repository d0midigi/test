# No encoding declaration

No encoding declaration

A page with no encoding information in HTTP, BOM, XML declaration or meta element will be treated as UTF-8.

The test on this page contains a div with a class name that contains the following sequence of bytes: `0xC3 0xBD 0xC3 0xA4 0xC3 0xA8`. These represent different sequences of characters in ISO 8859-15, ISO 8859-1 and UTF-8. The external, UTF-8-encoded stylesheet contains a selector:

```css
.test div.ýäè
```

This matches the sequence of bytes above when they are interpreted as UTF-8. If the class name matches the selector then the test will pass.

[Next test](/broken/pages/e4a7c44ccafa1440b24fb35df24c66ada4e5d0dc)

HTML5

the-input-byte-stream-015 [Result summary & related tests](file:///International/tests/html5/the-input-byte-stream/results-basics#basics) [Detailed results for this test](http://w3c-test.org/framework/details/i18n-html5/the-input-byte-stream-015) [Link to spec](http://www.w3.org/TR/html5/syntax.html#the-input-byte-stream)

Assumptions:

* The test is read from a server that supports HTTP.
