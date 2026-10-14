# UTF 8 BOM vs meta content

A page with a UTF-8 BOM will be recognized as UTF-8 even if the meta content attribute declares a different encoding.

The page contains an encoding declaration in a meta content attribute that attempts to set the character encoding to ISO 8859-15, but the file starts with a UTF-8 signature.

The test contains a div with a class name that contains the following sequence of bytes: 0xC3 0xBD 0xC3 0xA4 0xC3 0xA8. These represent different sequences of characters in ISO 8859-15, ISO 8859-1 and UTF-8. The external, UTF-8-encoded stylesheet contains a selector `.test div.ýäè`. This matches the sequence of bytes above when they are interpreted as UTF-8. If the class name matches the selector then the test will pass.

[Next test](/broken/pages/746f7a23d4b65993dd0877a233f888b91df05657)

## References

* HTML5 test identifier: the-input-byte-stream-037
* Result summary & related tests: /International/tests/html5/the-input-byte-stream/results-basics#precedence
* Detailed results for this test: http://w3c-test.org/framework/details/i18n-html5/the-input-byte-stream-037
* Link to spec: http://www.w3.org/TR/html5/syntax.html#the-input-byte-stream

{% hint style="info" %}
Assumptions:

* The default encoding for the browser you are testing is not set to ISO 8859-15.
* The test is read from a server that supports HTTP.
{% endhint %}
