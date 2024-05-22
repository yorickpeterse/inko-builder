# Builder

Builder allows generating of XML and HTML using an Inko DSL, without the need
for a template engine of sorts. It's inspired by the [Ruby "Builder"
project](https://github.com/tenderlove/builder), which does the same but in
Ruby.

# Requirements

- Inko 0.15.0 or newer

# Installation

```bash
inko pkg add github.com/yorickpeterse/inko-builder 0.12.0
inko pkg sync
```

# Examples

Generating a simple XML document:

```inko
import builder.xml (Document)
import std.stdio (STDOUT)

class async Main {
  fn async main {
    let out = STDOUT.new
    let doc = Document.with(fn (doc) {
      doc.element('person').with(fn (person) {
        person.element('name').text('Alice')
        person.element('city').text('Foo Town')
      })
    })

    out.print(doc.to_pretty_string)
  }
}
```

This produces the following XML:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<person>
  <name>Alice</name>
  <city>Foo Town</city>
</person>
```

Generating a simple HTML document:

```inko
import builder.html (Document)
import std.stdio (STDOUT)

class async Main {
  fn async main {
    let out = STDOUT.new
    let doc = Document.html('en', fn (html) {
      html.head.with(fn (head) { head.title.text('My website') })

      html.body.with(fn (body) { body.p.text('Hello!') })
    })

    out.print(doc.to_pretty_string)
  }
}
```

This produces the following HTML:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>My website</title>
  </head>
  <body>
    <p>Hello!</p>
  </body>
</html>
```

# License

All source code in this repository is licensed under the Mozilla Public License
version 2.0, unless stated otherwise. A copy of this license can be found in the
file "LICENSE".
