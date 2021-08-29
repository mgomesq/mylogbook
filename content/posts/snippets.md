---
title: snippets 
date: 2020-08-14 09:00:00
#cover:
#    image: "/img/mauri.jpeg"
#    # can also paste direct link from external site
#    # ex. https://i.ibb.co/K0HVPBd/paper-mod-profilemode.png
#    alt: "<alt text>"
#    caption: "<text>"
#    relative: false # To use relative path for cover image, used in hugo Page-bundles

ShowReadingTime: true
draft: true
---

### Inserting Jupyter nb 

Export to HTML, save it to static/nb/ and use following commands:
{{< rawhtml >}}
 <iframe
       src="/nb/Brain.html"
       width="100%"
       height="1000px"
       style="border:none;">
 </iframe> 
 {{< /rawhtml >}}


