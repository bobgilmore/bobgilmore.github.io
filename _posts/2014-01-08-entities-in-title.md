---
layout: post
title: HTML Entities in Jekyll Titles
tags:
- jekyll
- yaml
---
One of my posts had quotation marks in its title and it wasn't going well.  The Jekyll generator kept spewing errors like...

~~~~
YAML Exception reading <full path to file>: (<unknown>): 
did not find expected key while parsing a block mapping at line 2 column 1
~~~~

I found a simple workaround [here, on the Terry Hyde blog](http://blog.teddyhyde.com/2013/11/14/using-html-entities-inside-titles-with-jekyll/).  Just put the title with quotes on a separate line.  Rather than

~~~~
title: "Comments" in .railsrc
~~~~

or even

~~~~
title: &quot;Comments&quot; in .railsrc
~~~~

Use:

~~~~
title: |
    &quot;Comments&quot; in .railsrc
~~~~

Thanks Chris!