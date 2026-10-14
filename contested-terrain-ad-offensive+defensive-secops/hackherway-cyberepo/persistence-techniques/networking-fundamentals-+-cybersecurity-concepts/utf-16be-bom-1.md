# UTF 16BE BOM

A BOM (Byte Order Mark) for UTF-16 indicates byte order (endianness) and optionally marks a file as Unicode text.

* Name: UTF-16BE BOM (Big-Endian)
* Byte sequence (hex): FE FF
* Purpose: Signals that the file is UTF-16 encoded in big-endian byte order. Unlike UTF-8's BOM (EF BB BF), the UTF-16 BOM also conveys endianness.
* Notes:
  * The BOM is optional for UTF-16. If absent, you must know or detect the endianness by other means (protocol, metadata, heuristics).
  * When present in a UTF-16BE file, the first two bytes will be 0xFE 0xFF and should be interpreted as the BOM and typically not as part of the textual content.

Examples — detecting and handling

* View bytes (Linux/macOS):

```bash
xxd -g 1 file.bin | head
# or
hexdump -C file.bin | head
```

* Remove BOM (strip first two bytes) with dd:

```bash
dd if=input-utf16be.txt of=output-no-bom.txt bs=1 skip=2
```

* Convert to UTF-8 (iconv) and let iconv handle BOM:

```bash
iconv -f UTF-16BE -t UTF-8 input-utf16be.txt > output-utf8.txt
```

* Python (read as UTF-16BE and write UTF-8):

```python
with open('input-utf16be.txt', 'rb') as f:
    data = f.read()
# If you want to remove BOM explicitly:
if data.startswith(b'\xfe\xff'):
    data = data[2:]
text = data.decode('utf-16-be')
with open('output-utf8.txt', 'w', encoding='utf-8') as out:
    out.write(text)
```

If you want any specific examples (editing, converting, detecting in a particular environment or language), tell me which one and I’ll provide the exact commands or code.
