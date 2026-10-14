# UTF 16LE BOM

A BOM (Byte Order Mark) for UTF-16 little-endian (UTF-16LE) is a 2-byte sequence at the start of a text stream that indicates the encoding and byte order (endianness).

* BOM byte sequence (hex): FF FE
* BOM byte sequence (bytes): 0xFF, 0xFE

The presence of 0xFF 0xFE at the start of a file commonly signals UTF-16LE. Note that some tools and environments treat the BOM as part of the text (often as a zero-width no-break space) and it can cause problems when an application expects UTF-8 or ASCII input.

{% hint style="info" %}
A BOM is optional for UTF-16. Some systems (especially Windows) commonly write it; many Unix/Linux tools and protocols prefer BOM-less UTF encodings.
{% endhint %}

## Detecting the BOM

You can inspect the first bytes of a file to detect a UTF-16LE BOM.

Example (hex inspection):

* File starts with bytes: FF FE ... → likely UTF-16LE

Example commands:

* hexdump / xxd:

```
xxd -g 1 filename | head
```

Look for the initial bytes `ff fe`.

## Removing or skipping the BOM

If you need to remove or ignore the BOM, here are common approaches.

Python (read and remove BOM):

{% code title="remove_bom.py" %}
```python
# Read bytes and strip BOM if present
with open("file.txt", "rb") as f:
    b = f.read()
if b.startswith(b'\xff\xfe'):
    b = b[2:]
# decode as UTF-16LE if needed
text = b.decode('utf-16le')
```
{% endcode %}

Python (open with encoding that handles BOM):

{% code title="open_with_encoding.py" %}
```python
# 'utf-16' codec will auto-detect BOM and decode appropriately
with open("file.txt", "r", encoding="utf-16") as f:
    text = f.read()
```
{% endcode %}

Node.js (strip BOM if present):

{% code title="remove_bom.js" %}
```javascript
const fs = require('fs');
let buf = fs.readFileSync('file.txt');
if (buf[0] === 0xFF && buf[1] === 0xFE) {
  buf = buf.slice(2);
}
const text = buf.toString('utf16le');
```
{% endcode %}

Text editors/IDEs:

* Many editors provide save options to include or omit a BOM when saving a UTF-16 file. Look for encoding settings like “UTF-16 LE with BOM” vs “UTF-16 LE”.

## Common issues

* If a UTF-16LE BOM is present in a file expected to be UTF-8, the initial bytes will appear as garbled characters (or as the Unicode BOM character) and can break parsers.
* Some tools will auto-detect and handle BOMs, others will not—be explicit about encoding when reading files.

## Quick reference

* Name: UTF-16LE BOM
* Bytes (hex): FF FE
* Purpose: Marks UTF-16 encoding and little-endian byte order
* Optional: Yes

If you want examples for a specific language/tool not shown above, tell me which one and I'll add it.
