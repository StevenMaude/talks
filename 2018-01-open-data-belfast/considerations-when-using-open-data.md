# Considerations when finding and using "open" data

## Background

This was a presentation for the [TIMON Horizon 2020 EU
project](https://www.timon-project.eu/) hack weekend in Belfast that The
Sensible Code Company organised. The talk was given 2018-01-20. 

The context for the talk is that the TIMON project involved working with
both open and scraped city data, and we thought it was useful giving
attendees an overview on some of the things to think about when working
with this type of data.

Some non-important image slides were removed from the slides for ease of
licensing, and one image was adjusted (because for some reason I used a
deliberately glitched image, but I preferred the original on
reflection). These were really just visual prompts anyway.

I tidied up and edited the notes into this Markdown format in October
2020 for sharing.

## Spoiler: No solutions; some suggestions, but no solutions.

But I can highlight the issues! Being aware of boundaries is useful as
it stops you hurtling into walls. Maybe useful to open up to debate at
end.

## Data is everywhere, but may be more or less useful.

* People sometimes assume that "data on the web" is open: I can see and
  work with it! So it must be open!
* [Truly open
  data](https://blog.okfn.org/2013/10/03/defining-open-data/) is
  > freely used, shared and built-on by anyone, anywhere, for any
  > purpose

## A number of barriers

There are a number of barriers to using data on the web. We can use the
OKFN's definition of "truly open data" to highlight where those aspects
of open data might clash with real-world problems:

* Is the data available? < *shared*
* What licence does the data have? < *freely used*, *shared*
* How discoverable is the data? < *shared*
* How can I collect the data < *built-on*
* How consistent is the data? < *built-on*
* How much maintenance do I need to do to sustain this data pipeline? <
  *built-on*

### Availability

* Some data may not be available at all. In some cases, even
  though publicly funded bodies are involved with that work.
    * For example, local authorities not publishing traffic sensor data.
    * Another example that was topical (in winter when the talk was
      given): gritting truck locations. Some councils publish but not
      all.
* Effective data publishing can be time consuming/cost. There is a
  balance of public accountability against "do the number of users of
  that data justify the cost of preparing this data"?
* Data holders can be reluctant to publish because they think it’s an
  asset; e.g. GTFS feeds that most local transport authorities provide
  to Google (because they see that as a benefit to encourage users to
  take up their services), but won’t provide to public (or charge for,
  as we’ve found).
* Polite requests to the owner of data might work, if they’re
  sympathetic, and either: you can throw money at them (data providers
  may be missing out here), or the work to publish the data is limited
* In some jurisdictions and for public bodies, freedom of information
  (FOI) requests may be one way of getting data. But this is a slow
  process, and likely to get a one-off response, not large volumes of
  continuous streaming data (e.g. traffic sensor data).
* Sometimes, the motivation for publishing has to come from the data
  owner themselves, such as Data Mill North (Leeds City Council, later
  getting other councils involved), and seeing value not just in
  financial terms.

### Licensing

* In the same way that you can look through a shop window when the shop
  is closed, but behind a window barrier, data may be visible, but not
  open.
* It may not be explicitly licensed.
* If there is an explicit licence, it may be that you’re forbidden to
  reuse or even collect data.
* Language can be a problem, e.g. reading terms and conditions of a
  foreign language site. Web translators can help, but may not be
  completely accurate. 
* Without a license, collection and usage may be on dubious legal grounds, e.g.
  violating T&Cs/robots.txt in scraping. In practice, for a small,
  one-off personal project or analysis, no-one's likely to take legal
  action against you.
* But the legality of scraping is still not clear.

### Discoverability

* Even if available and published, data may not be easy to search for.
  * This depends on how well the publishers have optimised their content
    for search engines; what are users searching for versus how
    publishers describe it?
* Open data portals can help.
  * May have data portals that aren't easy to navigate; often general
    web searches are quicker to get to the data, but sometimes not if
    data is very niche.
* Language barriers can be tricky, e.g. for us collecting data from
  Slovenia, and having to use translation service to translate terms,
  which isn’t always perfect.
  * This exacerbates the searching problem if you don't speak the
    language.
  * Abbreviations can be particularly difficult to deal with.
* Sometimes easiest way is to have contacts or collaborators in
  organisations collecting data, or know people with domain expertise.
  In our case for TIMON, apart from searching ourselves, we had to
  request advice from those in the countries of interest (Netherlands
  and Slovenia).
 
### Data collection and formats

* May be common standards, with well maintained free, open source code
  to work with them.
  * May be variants on standards, or not fully implemented.
* May be arbitrary data dumps, in PDFs, Excel spreadsheets or the like,
  unlocking the data.
  * Sensible Code has some work in these areas to try and improve
    extraction:
    * PDFs: [PDFTables](https://pdftables.com/) to extract numerical
      data from PDFs (paid service; there are alternatives such as
      [Tabula](https://github.com/tabulapdf/tabula), that are open
      source.
    * Spreadsheets:
      [Databaker](https://github.com/sensiblecodeio/databaker/):
      processing spreadsheet data that can arbitrarily change (open
      source).
* May be data published directly to web, i.e. via HTML/JavaScript.
  * Various levels of complexity in scraping, from simple tables to more
    complex cases.
  * Scraping can be tedious and time-consuming to maintain if many
    sources, frequent site changes, odd site behaviour
  * May not be easily machine readable, e.g. unstructured/free text
    fields (e.g. charging point data for Belfast was a dump of text in
    KML format inside a `<description>` element.)
    * Also note that the full range of possible values in the data may
      not be documented or contained in the currently available data;
      have to just keep collecting data and handle new values as they
      arise. For instance, you may be asserting in data collection code that
      the data can only have one of a few values; a newly seen value may
      require particular handling.
  * Well-documented APIs with data in appropriate standard formats can
    help.
    * Good documentation needed for anyone to know what is accessible
      and how to access it
    * What's "appropriate"?
      * Appropriate for subject domain, e.g. traffic data has [DATEX
        II](https://www.datex2.eu/),
        e.g. [GTFS](https://developers.google.com/transit/gtfs) for
        public transport feeds.
      * Appropriate for users: simple to understand, availability of
        free, open source code in useful languages for working with that
        data.
      * If you are responsible for transforming data into a non-standard
        format into a standard format, that may only be successful if
        the standard form is flexible enough to accommodate your data.
      * You may also require assistance from domain experts on how best
        to represent your data. For instance, in the work we did at
        Sensible Code for TIMON, some of our data did not directly fit
        the DATEX II standard. We required some assistance from domain
        experts to add DATEX II extensions to best accommodate that
        data.

### Data consistency

* Data is often entered manually. You may have some cleaning of
  inconsistent data to do, and this cleaning may be an ongoing chore as
  the inconsistencies change.
* Different locations may offer different data and represent data in
  different ways. For example, we collected pollution data for Belfast
  and Ljubljana, and perhaps you get different data offered in different
  locations.
  * There may be more subtle issues to deal with such as working with
    the same kind of data, but where it is represented differently (e.g.
    different measurement users, metric versus imperial).

### Longevity

* How long will this data be available for? Indefinitely? Is your
  project/analysis a one-off thing, or designed to run continuously,
  like a web application?
* Ongoing use is more risky. Might the provider stop publishing in
  future? Are you relying on API keys from private, commercial companies
  who may change their terms and conditions? (e.g.  ScraperWiki — note
  this was The Sensible Code Company before rebranding — had their Twitter API
  [access
  revoked](https://scraperwiki.com/2014/08/the-story-of-getting-twitter-data-and-its-missing-middle/)).

## No easy fixes

These issues aren’t easy to solve generally!

Likely have to deal with this on a case-by-case basis. But it's
worthwhile to invest the time, since there’s a richness in combining
data sources to build or discover new things.
