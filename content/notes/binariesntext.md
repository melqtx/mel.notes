---
title: Binaries and text
description: talks about what are binary and text files
date: 2025-05-11
tags: 
- stable
enableToc: true
---
 # Binary vs Text Files: A Developer's Guide

## What Are Files Really?

At its core, every file on your computer is just a collection of bytes - numbers ranging from 0 to 255(some binary gibberish, if you dont know what 010001 is you are ngmi). Think of it like a long sequence of these numbers stored on your hard drive. However, how we interpret these bytes makes all the difference in the world.

Files come in two flavors: binary and text. Each has its own deal, and mixing ‘em up is a recipe for pain.

The fundamental distinction is this: Binary files can contain any byte pattern imaginable and require specialized software that understands their format (think Photoshop for images, VLC for videos). Text files, on the other hand, contain human-readable content and can be opened with any basic text editor.

While all files are technically binary at the lowest level, we treat text files differently because they follow certain conventions that make them readable. However, the reverse isn't true - if you treat a binary file like text, you'll likely corrupt your data. When all else fails, hex editors let you peek at the raw byte content of any file.

## Identifying File Types

The easiest way to guess a file's type is by looking at its extension. File extensions typically hint at the format, which determines whether the content is binary or text.

**Binary file extensions:**

- **Graphics:** jpg, png, gif, bmp, tiff, psd
- **Video:** mp4, mkv, avi, mov, mpg, vob
- **Audio:** mp3, aac, wav, flac, ogg, wma
- **Office docs:** pdf, doc, xls, ppt, docx, odt
- **Compressed:** zip, rar, 7z, tar, iso
- **Database:** mdb, sqlite, db
- **Programs:** exe, dll, so, class

**Text file extensions:**

- **Web tech:** html, xml, css, svg, json
- **Programming:** c, cpp, h, cs, js, py, java, rb, php, sh
- **Documentation:** txt, tex, markdown, rst, rtf
- **Settings:** ini, cfg, rc, reg, yaml
- **Spreadsheet data:** csv, tsv

## How Binary Files Work

Most everyday software deals with binary files. Applications like Microsoft Office, Adobe Creative Suite, and media players all consume and produce binary data. Regular users primarily work with binary files rather than text files.

Binary files need compatible software to be useful. An MP3 requires an audio player, a JPEG needs an image viewer, and so on. Some formats like JPEG have become so standard that many different programs support them - you can view JPEGs in browsers, photo editors, document processors, and even music players (for album artwork). However, proprietary formats might only work with one specific application.

Opening a binary file in a text editor results in gibberish - strange symbols, foreign characters, and extremely long lines. While viewing won't hurt anything, saving the file will destroy it. Text editors modify byte patterns when they try to "fix" what they perceive as text formatting issues, such as eliminating null bytes or converting line endings.

## How Text Files Work

Text files follow established conventions that make them human-friendly:

- Content appears readable or at least structured, even markup languages like HTML show clear patterns rather than random noise
- Information is typically organized line by line, with each line serving a specific purpose
- Special invisible characters are generally avoided (except common ones like tabs and newlines)
- Different line ending styles work interchangeably across platforms
- Character encoding determines how bytes beyond basic ASCII are interpreted

Text files offer several advantages:

- Universal compatibility - any text editor can open them
- Developer-friendly - programmers constantly work with text-based source code, configs, logs, and documentation
- Version control friendly - systems like Git can track changes line by line and merge modifications automatically
- Tool ecosystem - command-line utilities can easily process text data

Text files are usually displayed in monospaced fonts, originally due to terminal limitations but now because it helps align content visually for things like code indentation and data tables.

## Programming Examples

Different programming languages handle file types in their own ways, but the principle remains consistent across all of them.

**C Programming:**
```c
// text and binary handling, tho python is great for these tasks(only thing it is good at /s)
FILE *textFile = fopen("config.txt", "r");

FILE *binaryFile = fopen("photo.jpg", "rb");
```

**Python:**
```python
# Text file processing
with open('settings.txt', 'r', encoding='utf-8') as file:
    content = file.read()  # String output

# Binary file processing
with open('image.png', 'rb') as file:
    data = file.read()  # Bytes output
```

**Java:**
```java
// Text processing
FileReader textReader = new FileReader("data.txt");

// Binary processing
FileInputStream binaryStream = new FileInputStream("video.mp4");
```

**JavaScript (Node.js):**
```javascript
const fs = require('fs');

// Text processing
const textContent = fs.readFileSync('config.txt', 'utf8');

// Binary processing
const binaryData = fs.readFileSync('audio.mp3');
```


**Never edit binary files with text editors.** You can look at them (though you'll see nonsense, cuz you are retarded), but saving will corrupt the data. Text editors apply transformations that break binary file integrity.

**Always specify character encoding explicitly** when working with text files:

```python
# Risky - depends on system defaults
with open('file.txt', 'r') as f:
    data = f.read()

# Better - explicit encoding
with open('file.txt', 'r', encoding='utf-8') as f:
    data = f.read()
```

**Understand your data format.** If you're processing user uploads, validate the file type before attempting to read it as text or binary.

## Real-World Applications

**Configuration Management:**
```python
# Reading application settings (text)
with open('app.config', 'r') as f:
    for line in f:
        if line.startswith('database_host'):
            host = line.split('=')[1].strip()
```

**Image Processing:**
```python
from PIL import Image

# Working with image data (binary)
img = Image.open('original.jpg')
img.resize((800, 600))
img.save('resized.jpg')
```

**Data Analysis:**
```python
import csv

# Processing structured data (text)
with open('sales.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"Product: {row['name']}, Sales: {row['amount']}")
```

## Character Encoding Considerations

there are various encodings used by these files:

- **ASCII:** Basic English characters only (0-127)
- **UTF-8:** Universal standard supporting all languages
- **UTF-16:** Common in Windows environments
- **ISO-8859-1:** Legacy European encoding

utf-8 is your safest bet.

## File Signatures and Identification

Many binary formats include identifying markers at the beginning:

- **PNG:** Begins with bytes `89 50 4E 47`
- **JPEG:** Starts with `FF D8 FF`
- **PDF:** Opens with `%PDF-`
- **ZIP:** Begins with `50 4B`

you can examine all this usign some sort of cli tools.

```bash
# Unix/Linux systems
file mysterious_file.dat
hexdump -C suspicious_file.bin | head
```

## When to Choose Each Format

**Choose binary formats when:**
- File size matters (compressed images, audio, video)
- Processing speed is critical
- Working with complex data structures
- Building applications that need compiled code
d
**Choose text formats when:**
- Human readability is important
- Version control tracking is needed
- Cross-platform compatibility is required
- Debugging and troubleshooting are priorities

## Conclusion

Understanding file types isn't just academic knowledge - it's practical wisdom that prevents data loss and debugging nightmares. Binary files offer efficiency and complexity but require specialized tools. Text files provide transparency and universal compatibility at the cost of larger file sizes.

The key takeaway: respect the intended format of your files. Use appropriate tools and methods for each type, and you'll avoid most file-related problems in your development work.