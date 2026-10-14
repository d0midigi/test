# HTTP vs UTF 8 BOM

A character encoding set in the HTTP header has lower precedence than the UTF-8 signature.

The HTTP header attempts to set the character encoding to ISO 8859-15. The page starts with a UTF-8 signature.

The test contains a div with a class name that contains the following sequence of bytes:

```
0xC3 0xBD 0xC3 0xA4 0xC3 0xA8
```

These represent different sequences of characters in ISO 8859-15, ISO 8859-1 and UTF-8. The external, UTF-8-encoded stylesheet contains a selector:

```
.test div.ýäè
```

This selector matches the sequence of bytes above when they are interpreted as UTF-8. If the class name matches the selector then the test will pass.

{% hint style="warning" %}
If the test is unsuccessful, the characters ï»¿ should appear at the top of the page. These represent the bytes that make up the UTF-8 signature when encountered in the ISO 8859-15 encoding.
{% endhint %}

Next test: [generate?test=the-input-byte-stream-022](/broken/pages/92873fc9c6d92a3dda9d011ea4f63aeefc5188f0)

***

HTML5

Test: the-input-byte-stream-034

* [Result summary & related tests](file:///International/tests/html5/the-input-byte-stream/results-basics#precedence)
* [Detailed results for this test](http://w3c-test.org/framework/details/i18n-html5/the-input-byte-stream-034)
* [Link to spec](http://www.w3.org/TR/html5/syntax.html#the-input-byte-stream)

Assumptions:

* The default encoding for the browser you are testing is not set to ISO 8859-15.
* The test is read from a server that supports HTTP.
