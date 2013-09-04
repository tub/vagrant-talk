class: center, middle

# Solr &amp; Content Recommendation

![Solr Logo](solr_logo_rgb.png)

Toby Cole, Technical Architect, Semantico

---

# What am I talking about?

* What are Lucene &amp; Solr?
* Tokenization, terms and term-filters.
* Relevance - tf-idf algoithm
* Solr's API
* More Like This
* Sharded More Like This (hopefully)

---

# What are Solr &amp; Lucene?

## Lucene
* Java full-text search library
* Started in '99
* Documents, fields, text.

## Solr
* REST API on top of Lucene
* Adds field-types & schema
* Nice client library, SolrJ

---


# Tokenization &amp; terms
Given a sentence:

`An ASCII representation of Miley Cyrus' twerking face ;P`

tokenization is splitting into indexable chunks

`An` `ASCII` `representation` `of` `Miley` `Cyrus` `twerking` `face` `P`

term-filters can be used to modify these terms before they're indexed

lowercasing:

`an` `ascii` `representation` `of` `miley` `cyrus` `twerking` `face` `p`

stemming:

`an` `ascii` `represent` `of` `milei` `cyru` `twerk` `face` `p`

# tf-idf

See [Lucene's TFIDF Javadoc](http://lucene.apache.org/core/4_4_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) for a good description

## Term Frequency

Many occurences in one document == **relevant to document**

## Inverse Document Frequency

* Rare terms == **relevant**
* Common terms == **not relevant**

## Field length

* Shorter == **better**

(This is a massive oversimplification, deal with it.)

---
# Solr's API - Input
Various formats available:

* XML
* JSON
* CSV
* Streaming binary content + Tika (Doc, PDFs etc)
* Database Import

---
# Solr's API - Input XML

Over HTTP - 
`POST /update`

```xml
<add>
  <doc>
    <field name="employeeId">05991</field>
    <field name="office">Bridgewater</field>
    <field name="skills">Perl</field>
    <field name="skills">Java</field>
  </doc>
  [<doc> ... </doc>[<doc> ... </doc>]]
</add>
```


more details - [Solr Update docs](http://wiki.apache.org/solr/UpdateXmlMessages)

---
