---
layout: post
title:  "Scraping a Website with Nokogiri and Open-URI (in Ruby)"
date:   2017-08-29 22:21:34 +0000
---


Scraping is a way for Ruby programs to get data from external sources on the web by grabbing data out of the HTML of a website. For instance, you might build a simple CLI application that retrieves a list of new movies playing in your theatre nearby.
It can be a little complicated at first but once you get the hang of it it’s quite easy, especially if you’re already familiar with HTML and CSS. 

## What Do You Need to Get Started?
Open-URI and Nokogiri. Open-URI is a Ruby module that allows you to make HTTP requests and the Nokogiri gem helps you parse that retrieved HTML and collect data from it.
Install Nokogiri following these [installation instructions](http://www.nokogiri.org/tutorials/installing_nokogiri.html), then “require” Nokogiri and Open-URI in your Ruby file.
```
require 'nokogiri'
require 'open-uri'
```

Save your target website's HTML into a variable and convert it into a NodeSet (nested nodes) with Nokogiri (save the NodeSet into another variable).
```
html = open("https://xkcd.com/")
doc = Nokogiri::HTML(html)
```
Or combine these two into one:
```
doc = Nokogiri::HTML(open("https://xkcd.com/"))
```

Using 'puts' on that variable would give us something like this:
```
<!DOCTYPE html>
<html>
<head>
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');
  ga('create', 'UA-25700708-7', 'auto');
  ga('send', 'pageview');
</script>
<link rel="stylesheet" type="text/css" href="/s/b0dcca.css" title="Default">
<title>xkcd: Color Models</title>
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<link rel="shortcut icon" href="/s/919f27.ico" type="image/x-icon">
<link rel="icon" href="/s/919f27.ico" type="image/x-icon">
<link rel="alternate" type="application/atom+xml" title="Atom 1.0" href="/atom.xml">
<link rel="alternate" type="application/rss+xml" title="RSS 2.0" href="/rss.xml">
<script type="text/javascript" src="/s/b66ed7.js" async></script>
<script type="text/javascript" src="/s/1b9456.js" async></script>
</head>
<body>
<div id="topContainer">
<div id="topLeft">
<ul>
<li><a href="/archive">Archive</a></li>
<li><a href="http://what-if.xkcd.com">What If?</a></li>
<li><a href="http://blag.xkcd.com">Blag</a></li>
```

A little confusing? Let’s get only the element that we want from that HTML code. Go to your target website, inspect the element you want to pull data from, and use the desired CSS selector to select the element with Nokogiri.
![XKCD Inspect Element](http://i.imgur.com/Mo9bGmp.jpg)
```
doc.css("div#ctitle")
```
When we 'puts' that out, we get this:
```
<div id="ctitle">Color Models</div>
```

Much better, but we still need to select just the specific text from that element:
```
doc.css("div#ctitle").text     # "Color Models"
```

And there you have it, your title.
## An Example
To get the first title on reddit, you can try something like this:

```
# Require libraries/modules
require 'nokogiri'
require 'open-uri'

# Create your scraper class
class Scraper

  # Get the HTML from your desired website
  def get_page
    doc = Nokogiri::HTML(open("https://www.reddit.com/"))
  end
  
	# Define where your saught after element is and 'puts' it out
  def print_first_title
    first_title = self.get_page.css("a.title.may-blank").first.text
    puts first_title
  end

end

# Call your method
Scraper.new.print_first_title

```

Of course there are way more advanced methods to scrape the data you want and many different things to do with that data, but that's topic for another time.

### References
* [The Bastards Book of Ruby::Parsing HTML with Nokogiri](http://ruby.bastardsbook.com/chapters/html-parsing/)
* [Nokogiri::Parsing an HTML/XML Document](http://www.nokogiri.org/tutorials/parsing_an_html_xml_document.html)


