---
title: YATTAG
description: Generate HTML or XML in a pythonic way. Pure python alternative to web template engines.Can fill HTML forms with default values and error messages.
published: true
date: 2020-04-19T03:34:53.447Z
tags: html, xml, tag, tags
---

```python
from yattag import Doc, indent

doc, tag, text = Doc().tagtext()

with tag('html'):
    with tag('body'):
        with doc.tag("link", rel="stylesheet", href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css", integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T", crossorigin="anonymous"):
            pass
        with doc.tag("h1"):
            doc.text("hola mundo")

        with doc.tag("table", klass="table table-striped"):
            with doc.tag("thead"):
                with doc.tag("tr"):
                    with doc.tag("th", scope="col"):
                        doc.text('#')
                    with doc.tag("th", scope="col"):
                        doc.text('First')
            with doc.tag("tbody"):
                with doc.tag("tr"):
                    with doc.tag("th", scope="row"):
                        doc.text('1')
                    with doc.tag("td"):
                        doc.text('Mark')
                
                
            
        with doc.tag("script", src="https://code.jquery.com/jquery-3.3.1.slim.min.js", integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo", crossorigin="anonymous"):
            pass
        with doc.tag("script", src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js", integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1", crossorigin="anonymous"):
            pass
        with doc.tag("script", src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js", integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM", crossorigin="anonymous"):
            pass
        with tag('p', id = 'main'):
            text('some text')
        with tag('a', href='/my-url'):
            text('some link')

            
result = doc.getvalue()

# raw print
print(result)
# will indent the tags but not the text directly contained between <tag> and </tag>
print(indent(doc.getvalue())) 
# will also indent the text directly contained between <tag> and </tag>
print(indent(doc.getvalue(), indent_text = True))

```