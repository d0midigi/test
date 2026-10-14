# meta content attribute

The character encoding of the page can be set by a meta element with `http-equiv` and `content` attributes.

The only character encoding declaration for this HTML file is in the `content` attribute of the meta element, which declares the encoding to be ISO 8859-15.

The test contains a `div` with a class name that contains the following sequence of bytes: `0xC3 0xBD 0xC3 0xA4 0xC3 0xA8`. These represent different sequences of characters in ISO 8859-15, ISO 8859-1 and UTF-8. The external, UTF-8-encoded stylesheet contains a selector `.test div.ÃœÃ€Ãš`. This matches the sequence of bytes above when they are interpreted as ISO 8859-15. If the class name matches the selector then the test will pass.

Next test: [generate?test=the-input-byte-stream-009](/broken/pages/56d1e8671f820ecae310d0b1441c1f88fdab77c1)

HTML5

Links:

* [Result summary & related tests](file:///International/tests/html5/the-input-byte-stream/results-basics#basics)
* [Detailed results for this test](http://w3c-test.org/framework/details/i18n-html5/the-input-byte-stream-007)
* [Link to spec](http://www.w3.org/TR/html5/syntax.html#the-input-byte-stream)

{% hint style="info" %}
Assumptions:

* The default encoding for the browser you are testing is not set to ISO 8859-15.
* The test is read from a server that supports HTTP.
{% endhint %}
