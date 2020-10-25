---
title: Spiders and Robots? Web Crawling and Scraping!
date: 2020-10-21 09:00:00
tags:
- Web Scraping
- Web Crawling
keywords:
    - crawling
    - scraping
    - web
---

## Introduction
Many people still get confused about what is web scraping and web crawling, and if you are one of them, don’t worry, that’s ok. Even though it is all about extracting data from the web, there are differences between them, and knowing them will make you best suited for the future. In this article, I will present the definitions and how they can be applied. 

Web scraping is an automated gathering of data from internet websites. Think of opening a web browser to see your favorite movie rating on a review website, only it is not you who is fetching that information but a computer program. As a rule of thumb, if you can see it in your browser, you can use a program to access, store, and analyze it. By using a computer, large amounts of data can be obtained (scraped) from internet pages rather quickly. One common usage is in sentiment analysis of scraped data from forums and social media.  

Web scraping often goes hand in hand with web crawling. A Crawler (also known as a robot, spider, bot, etc.) is a program that indexes websites by following links. From a set of initial URLs, it requests each one of it and takes note of every hyperlink contained in the response. Then it follows the hyperlinks only to repeat the process. Web crawling is now a part of every internet user’s life. If you use a search engine to browse websites, you have queried from a list of indexed pages gathered by a crawler. Google, for example, reports having hundreds of billions of pages indexed ([as of 2020](https://www.google.com/search/howsearchworks/crawling-indexing/)). A similar use is in web archiving (such as the [Internet Archive](https://archive.org/)), where many web pages are crawled and stored over time to provide historical data for future reference.   

Web crawling is a good method for page indexing and when coupled with web scraping, you have yourself a bot that can look through large amounts of data stored on different websites.  
Setbacks and legal considerations  

## Setbacks and legal considerations  

Companies often use these techniques to gain a competitive advantage (such as in price monitoring their competitors) or to provide services based on the gathered data, in such a way that even when web scraping collects publicly available information, it is not always welcome. Legally nowadays scraping and crawling stands in a grey area, with recent advances in court ([HiQ Labs v. LinkedIn](https://law.justia.com/cases/federal/appellate-courts/ca9/17-16783/17-16783-2019-09-09.html)) claiming that automated access to publicly available data is not a violation of the Computer Fraud and Abuse Act (CFAA).  

Put aside ethical and legal issues, crawlers can be harmful if not controlled or used properly. They can impose excessive traffic on a website that is not ready for it, performing an “innocent” denial-of-service attack, or at best case scenario consuming a lot of bandwidth, forcing the site owner to pay more to accommodate the scrapers activity.  

Nothing stops developers from building technical protection mechanisms around their websites, such as CAPTCHAS, logins, and header checks. Some sites will even block you if you interact with them too quickly as a robot would do. All the techniques used as protection try to discern real people from bots. Some of them can be difficult to fool, some not so much. Nonetheless, the barrier they make can impose serious setbacks in successfully scraping a website.  
Conclusion

## Conclusion

Nowadays there are many extremely useful applications involving web crawling and web scraping. Think of all the information that is available online, waiting to be scraped and analyzed!  

Whether or not it fits your needs right now, the techniques discussed here are becoming increasingly a part of every business decision, and though vast in possibilities, one should tread carefully to not fall into legal traps.
