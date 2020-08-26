---
title: Web Scraping in Python - Scraping Dwarf Fortress Creatures
date: 2020-08-14 09:00:00
tags:
- Python
- Web Scraping
- Web Crawling
- Dwarf Fortress 
categories:
- Python
keywords:
    - Algorithms
    - String
    - radix sort
---


## Dwarf Fortress

I've lately been caught up in playing **Dwarf Fortress** with my brother. The game is a single-player simulation where you control a dwarven outpost in a randomly generated world [^1].

It's a rough game, really challenging. Nonetheless, [fun](https://dwarffortresswiki.org/index.php/Fun). The way we would play it is one of us would open the Dwarf Fortress Wiki [^2] and feed the other, who's actually controlling the game, informations about it's world.

The Wiki is pretty useful when you are trying to find out on the run whether that Chinchilla Man you just saw is hostile or not. But what if you don't want to open a browser every time you want to find it out? Or if you want to use that information locally for something?

With the game nowadays having up to 700 different creatures, you surely won't mannualy gather that information for yourself.

## Web Scraping and Web Crawling

Well you can create a program to extract the data you want from the website in an automated fashion. We call this **Web Scraping**. Now, Web Scraping often goes hand in hand with **Web Crawling**, and that's when you, from a base page, start to follow links and also visit other pages. Web crawlers are also widely reffered to as bots or spiders.

### Scraping Creatures

 If you head to the [Creature](https://dwarffortresswiki.org/index.php/DF2014:Creature) page of the Dwarf Fortress Wiki, you'll see tables  containing informations about each creature of the game. There's a name and hostile fields. That's the information we are looking for.

{{< figure src="/img/dwarf_fortress_table.png" height=1000 width=1000 >}}

 <!-- You should be able to see that each creature on the table has a link to a page, and they all share the same domain.

 ```
https://dwarffortresswiki.org/index.php/DF2014:Dwarf
https://dwarffortresswiki.org/index.php/DF2014:Elf
https://dwarffortresswiki.org/index.php/DF2014:Goblin
https://dwarffortresswiki.org/index.php/DF2014:Human
(...)

 ``` -->


### Scrapy
Scrapy is an open source framework for Web Scraping and Web Crawling in Python[^3]. Using Scrapy makes it easy to request and parse HTML, as it handles a lot of it for us. It's simple to set it up and get it running. Let's dive right in to it!

To install it, simply open a terminal and 

```
pip install scrapy
```

The first thing to do when working with Scrapy is to set up the framework for our spiders, which can be done through the command ```scrapy startproject``` followed by the project name. I will call my project 'dwarf_fortress' so,

```
scrapy startproject dwarf_fortress
```

Scrapy will **create generic folders, code and config for our crawlers**. The structure will be something like:

```

────dwarf_fortress
    │   scrapy.cfg
    │
    └───dwarf_fortress
        │   items.py
        │   middlewares.py
        │   pipelines.py
        │   settings.py
        │   __init__.py
        │
        ├───spiders
        │   │   __init__.py
        │   │
        │   └───__pycache__
        └───__pycache__

```

Now that we've created a project, let's go into the directory 'dwarf_fortress' and run another command to make Scrapy set up a generic spider for us. That's a good starting point.

I'll name it 'Creatures' and say that the base url is ['dwarffortresswiki.org/index.php/DF2014:Creature'](https://dwarffortresswiki.org/index.php/DF2014:Creature).

```
cd dwarf_fortress
scrapy genspider Creatures dwarffortresswiki.org/index.php/DF2014:Creature

```

You should be able to see the created spider as a new file in the 'spiders' folder called ``` Creatures.py ```.

```python
# Creatures.py
# -*- coding: utf-8 -*-
import scrapy


class CreaturesSpider(scrapy.Spider):
    name = 'Creatures'
    allowed_domains = ['dwarffortresswiki.org/index.php/DF2014:Creature']
    start_urls = ['http://dwarffortresswiki.org/index.php/DF2014:Creature/']

    def parse(self, response):
        pass


```

The class CreaturesSpider represents the spider that will grab each creature name hostile information from the Wiki. ```AllowedDomains``` restrict the domain of sites the spider can visit. 
<!-- Let's delete that last part and leave it restricted at 'index.php' -->

Notice that the start url has 'http' protocol, while the Wiki uses 'https'. That alone will make our spider crash, so be sure to fix it.

Our spider will request the ```start_url``` and pass the HTTP response to the ```parse``` method. And that's where we'll code to fetch the data we need.

But first we need to define the structure of the information we are collecting. We can do it in the ```items.py``` file. There, we define Classes that represent the information as 'scrapy.Items' which are the containers for the data scrapped. Let's add a ```name``` and ```hostile``` field. 

```python

# -*- coding: utf-8 -*-
# Define here the models for your scraped items
import scrapy

class DwarfFortressItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()

    name = scrapy.Field()
    hostile = scrapy.Field()

```

Now, the last thing we need to do before running the crawler, is to tell our spider **where** are the name and hostile fields in the HTTP response.

### Xpath 

We can use Xpath syntax in Scrapy to grab only the elements we need from the page.

By opening the Wiki ['Creature page'](https://dwarffortresswiki.org/index.php/DF2014:Creature) in a web browser, we can right click one creature's Hostile field and go to Inspect Element. 

{{< figure src="/img/dwarf_fortress_creature_xpath_table.png" height=500 width=500 >}}
{{< figure src="/img/dwarf_fortress_creature_xpath.png" height=500 width=500 >}}

Now, we have to write the path to each field. We start from the outside to the inside, so we first grab every row of every table that has a class 'wikitable sortable jquery-tablesorter'. In Xpath, 

row -> ```//table[@class='wikitable sortable jquery-tablesorter']/tbody/tr```

Now, for every row, we take the text of the second element (notice that the text for the 'name' element is located at 'td/a') and the text of the fourth element.

name (inside row)->  ```./td[2]/a/text()```

hostile (inside row) ->  ```./td[4]/text()```

### Putting it all together

Heading back to the parse method, we import our DwarfFortressItem and write the logic to fetch name and hostile from the response.

```python

# -*- coding: utf-8 -*-
import scrapy
from dwarf_fortress.items import DwarfFortressItem

class CreaturesSpider(scrapy.Spider):
    name = 'Creatures'
    allowed_domains = ['dwarffortresswiki.org/index.php']
    start_urls = ['https://dwarffortresswiki.org/index.php/DF2014:Creature']

    def parse(self, response):

        table_rows = response.xpath("//table[@class='wikitable sortable jquery-tablesorter']/tbody/tr")
        
        for row in table_rows:
            name = row.xpath("./td[2]/a/text()").get()
            hostile = row.xpath("./td[4]/text()").get()

            if name and hostile:
                creature = DwarfFortressItem(name=name, hostile=hostile.strip('\n'))
                yield creature

```

If name and hostile are not null (that avoids returning other page elements that may happen to match the Xpath), we yield our DwarfFortressItem defined previously.

To run our crawler and save the output to a json file,

```scrapy crawl Creatures -o output.json ```

And that's it! Looking at the output's first elements, we've successfully scraped the Dwarf Fortress Wiki for Creature name and Hostile information!

```json
[
{"name": "Dwarf", "hostile": "No"},
{"name": "Elf", "hostile": "Variable"},
{"name": "Goblin", "hostile": "Usually"},
{"name": "Human", "hostile": "Variable"},
{"name": "Kobold", "hostile": "Usually"},
{"name": "Amphibian man", "hostile": "Variable"},
{"name": "Antman", "hostile": "Variable"},


```



[^1]: http://www.bay12games.com/dwarves/
[^2]: https://dwarffortresswiki.org/
[^3]: https://scrapy.org/