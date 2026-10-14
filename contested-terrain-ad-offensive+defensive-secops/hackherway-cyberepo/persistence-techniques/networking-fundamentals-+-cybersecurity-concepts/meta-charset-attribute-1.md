# meta charset attribute

The character encoding of the page can be set by a meta element with the `charset` attribute.

The only character encoding declaration for this HTML file is in the `charset` attribute of the meta element, which declares the encoding to be ISO 8859-15.

The test contains a `div` with a class name that contains the following sequence of bytes:

```
0xC3 0xBD 0xC3 0xA4 0xC3 0xA8
```

These bytes represent different sequences of characters in ISO 8859-15, ISO 8859-1 and UTF-8. The external, UTF-8-encoded stylesheet contains a selector:

```css
.test div.ÃœÃ€Ãš
```

This selector matches the sequence of bytes above when they are interpreted as ISO 8859-15. If the class name matches the selector then the test will pass.

HTML5 — the-input-byte-stream-009

Related links:

* [Result summary & related tests](file:///International/tests/html5/the-input-byte-stream/results-basics#basics)
* [Detailed results for this test](http://w3c-test.org/framework/details/i18n-html5/the-input-byte-stream-009)
* [Link to spec](http://www.w3.org/TR/html5/syntax.html#the-input-byte-stream)

Assumptions:

* The default encoding for the browser you are testing is not set to ISO 8859-15.
* The test is read from a server that supports HTTP.
