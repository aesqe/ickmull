# ickmull

**Automatically exported from http://code.google.com/p/ickmull**

Ickmull is a tool to turn web content into a format for Adobe [InDesign](https://github.com/aesqe/ickmull/wiki/InDesign). More concretely, it is an XSLT transform for taking basic prose text in XHTML format (from a blog or wiki, for instance) and converting it to the open, XML-based ICML format (a subset of the full IDML spec) so the content can be migrated automatically into Adobe InDesign layouts. This transform and the accompanying testing framework are specifically designed to encourage user's to extend the of a core set of functionality. 

Ickmull is designed to be a starting place for a publisher-specific web-to-print production path. It aims to do all the basic things while remaining simple and flexible enough to be customized for specialized contexts. 

This project spearheaded by John Maxwell at the [Simon Fraser University's Master of Publishing Program](http://tkbr.ccsp.sfu.ca/research/xml-production), with much help from [Keith Fahlgren](http://threepress.org/about/#keith) of [Threepress](http://threepress.org). 

* * *

Basic how-to: 

1. You need to start with plain XHTML content. Ickmull has been developed using [WordPress](https://github.com/aesqe/ickmull/wiki/WordPress)'s export (and its visual editor) as a kind of reference standard for XHTML generation. It may not work as well with arbitrary web content from wherever, but it should work pretty well on anything that WordPress or the TinyMCE editor has produced. 

2. I've made available (see Downloads) a very minimal WordPress **plugin** to save out just the content of a page or post. Save the XHTML to your filesystem and you should be able to use Ickmull directly. You could also do this by cutting and pasting content out of your CMS, or writing it by hand. Note that XSLT processors like XHTML to be represented as proper XML, so an XML declaration at the top is needed (the plugin puts this in automatically): 
> &lt;?xml version="1.0" encoding="utf-8" ?&gt;

3. Now run the script on your HTML, and save the results as an .icml file. Using [xsltproc](https://github.com/aesqe/ickmull/wiki/xsltproc) (which you will find on your Mac, or in Linux), this looks like so: 
<pre class="prettyprint"><span class="pln">&nbsp; &nbsp;xsltproc </span><span class="pun">--</span><span class="pln">output myNewFile</span><span class="pun">.</span><span class="pln">icml </span><span class="pun">--</span><span class="pln">novalid tkbr2icml</span><span class="pun">-</span><span class="pln">v04x</span><span class="pun">.</span><span class="pln">xsl myWebPage</span><span class="pun">.</span><span class="pln">html</span></pre>

I always run it with <tt>--novalid</tt> to avoid attempting to laboriously validate the XHTML content... You can validate it it you want; I usually just trust WordPress to give me usable XHTML. 

If you don't have <tt>xsltproc</tt> (part of the ubiquitous libxml tools), read more at xsltproc. <tt>xsltproc</tt> is simple and it works, so that's what I'm suggesting here. 

4. The resulting file **should** be a valid Adobe [InCopy](https://github.com/aesqe/ickmull/wiki/InCopy) file. You import it into InDesign by **placing** it in an existing document. If you place it in a new blank document, InDesign should automatically create all the Paragraph and Character styles named in the <tt>.icml</tt> (based on what you had in the HTML, including <tt>class</tt> names for paragraphs and spans). But in a new InDesign doc, they won't look like anything, so you'll need to spend some time defining the style attributes... If you then save those out in an InDesign Template, you can place your next icml file into a Template and the styles should magically come to life.

> - JMax, Nov 2011.
