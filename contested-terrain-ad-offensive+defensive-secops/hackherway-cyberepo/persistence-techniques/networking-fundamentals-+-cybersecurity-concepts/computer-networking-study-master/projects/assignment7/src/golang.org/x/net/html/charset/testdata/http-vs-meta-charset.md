# HTTP vs meta charset

The HTTP header has a higher precedence than an encoding declaration in a meta charset attribute.

The HTTP header attempts to set the character encoding to ISO 8859-15. The page contains an encoding declaration in a meta charset attribute that attempts to set the character encoding to ISO 8859-1.

The test contains a div with a class name that contains the following sequence of bytes:

```
0xC3 0xBD 0xC3 0xA4 0xC3 0xA8
```

These represent different sequences of characters in ISO 8859-15, ISO 8859-1 and UTF-8. The external, UTF-8-encoded stylesheet contains a selector:

```
.test div.ÃœÃ€Ãš
```

This matches the sequence of bytes above when they are interpreted as ISO 8859-15. If the class name matches the selector then the test will pass.

Next test: [generate?test=the-input-byte-stream-037](/broken/pages/84fd3485eb00d9c91d27e1f3ce47e29cd47b93ea)

## Context / references

* HTML5
* Test: the-input-byte-stream-018
* [Result summary & related tests](file:///International/tests/html5/the-input-byte-stream/results-basics#precedence)
* [Detailed results for this test](http://w3c-test.org/framework/details/i18n-html5/the-input-byte-stream-018)
* [Link to spec](http://www.w3.org/TR/html5/syntax.html#the-input-byte-stream)

{% hint style="info" %}
Assumptions:

* The default encoding for the browser you are testing is not set to ISO 8859-15.
* The test is read from a server that supports HTTP.
{% endhint %}
