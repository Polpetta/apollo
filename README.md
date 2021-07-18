# Apollo 💎
### The first search engine where you choose what content to put in
### A personal search engine for a footprint you create!

Apollo is a different type of search engine. Traditional search engines (like Google) are great for **discovery** when you're trying to find the answer to a question, but you don't know what you're looking for.

However, they're very poor at **recall and synthesis** when you've seen something before on the internet somewhere but can't remember where. Trying to find it becomes a nightmare - how can you synthezize the great material on the internet when you forgot where it even was? I've wasted many an hour combing through Google and my search history to look up a good article, blog post, or just something I've seen before.

Even with built in systems to store some of my favorite [articles](https://zeus.amirbolous.com/articles), [podcasts](https://zeus.amirbolous.com/podcasts), and other stuff, I forget things **all the time**.

## Thesis
Screw finding a needle in the haystack. Let's create a new type of search to **choose which gem you're loking for**

Apollo is a search engine to digest **your digital footprint**. What this means is that **you choose what to put in it**. When you come across something that looks interesting, be it an article, blog post, website, whatever, you **manually add it** (with built in systems to make doing so easy). This tackles one of the biggest problems of recall in search engines returning a lot of irrelevant information because with Apollo, **the signal to noise ratio is very high**. You've chosen **exactly what to put in it**.

Apollo is not necessarly built for raw discovery (although it certainly matches rediscovery), it's built for knowledge compression and transformation - that is looking up things that you've previously deemed to be cool

## High level tasks
1. Full-text search algorithm
2. Data sources, how to ingest data from different sources? Just a text box where you post link, text, (and optional tags?)

## Data Schema
Two schemas we use, one to first parse the data into some encoded format. 
This does not get stored, it's purely an intermediate before we transform it into a record for our inverted index.
Why is this important?
- Because since any data gets parsed into this standarized format, you can link **any data source** you want, if you build your own tool, if you store a lot of data in some existing one, you don't have to manually add everything. *Just write small script that pulls the data*? (or should this provided in the search engine)
```go
type Data struct {
    title string //a title of the record, self-explanatory
    link string //links to the source of a record, e.g. a blog post, website, podcast etc.
    content string //actual content of the record, must be text data
    tags []string //list of potential high-level document tags you want to add that will be
                  //indexed in addition to the raw data contained 
}
```

```go
type Record struct {
    
}
```

Store indexes as such. We avoid storing the raw data, favoring to store and recompute the inverted index (like the index at the back of a book with a list of words that references different pages)

**Notes** 
- Inverted index generated at build time, like [monocole](https://github.com/thesephist/monocle), since this means I don't have run it on my server and can save money. 
- Small script that redeploys the website at intermittent periods, don't have to do it manually
- Since this is not a commercial product, I will not be running your *version of this* (if you find it useful) on my server. However, althought I designed this, first and foremost for myself, I want other people to be able to use if this is something that's useful.
- Pipeline:
Ingest data -> Convert raw data into records, which are stored in the inverted index -> Client uses inverted index (with some text processing shenanagins like stemming and lexing and that stuff) to load results

1. Client (search engine) is a static deployment
2. Backend which converts raw data into records and does all the heavyweight text parsing is written in Go which runs on your local machine (saving both me and you server costs!)
3. How do we ingest data? Unsure of this bit

### Workflows
1. If it's an article, need to paste the body of the article
2. If it's a podcast episode, transcribe it with [oTranscribe](https://otranscribe.com/) then put it in


## Document storage
TODO