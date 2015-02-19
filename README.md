# omicsGraph
The purpose of this repo is for me to try out Neo4j. The content of this repo has been shamelessly borrowed/inspired from the following awesome people.

* [Nicole White](https://github.com/nicolewhite/graphs_r_cool) - RNeo4j Tutorials
* [Nigel Small](https://github.com/nigelsmall/py2neo) - py2neo module
* [Max De Marzi](http://maxdemarzi.com/) - Neo4j

Thank You!

---

## Dependencies
* R version 3.1.2 "Pumpkin Helmet"
	* RNeo4j
	* igraph
* Python version 2.7.9
	* requests
	* py2neo version 2.0.2
* Neo4j version 2.1.6
* OS:

	![About my Mac](images/about_this_mac.png)


## Set up your own Twitter app
* Obtain a `consumer_key` and a `consumer_secret` by [registering](https://dev.twitter.com/apps) an application on twitter.
* Get a [bearer token](https://dev.twitter.com/docs/auth/application-only-auth), type the following in your terminal:

```
curl -XPOST -u consumer_key:consumer_secret 'https://api.twitter.com/oauth2/token?grant_type=client_credentials'
```

* Copy **just** the token from the output of the previous command and execute the following command

```
export TWITTER_BEARER="the twitter bearer returned from the previous line"
```

### Collect and Load data into Neo4j
Launch `neo4j`, taking note of which `port` you're running it on. 
The script `collect_keyword.py` will collect the tweets related to your `hashtags` and simultaneously populate the neo4j database running in the background. By default, the script will run for 2000 successful attempts of data retrieval, where `success` is defined as any number of tweets received. This is how you can use the script:

```
python collect_keyword.py port hashtag [success]
```

**NOTE:** **Do not** use the symbol `#` when asking for a `hashtag` in the command above.

If you're running at `http://localhost:7474/db/data/`, you can start populating the database with:

```
python collect_keyword.py 7474 omics 20
```
The first argument, `7474`, is the port you're running neo4j on, the second argument, `omics`, is the `keyword` or `hashtag` by which you want to search for tweets and the third argument, `20` is the number of successful attempts you would want the script to make.
You may run this command with a different keyword as many times as you wish. In my case, I used the port 2794, with a few hashtags and let it run for the default number of successes. So the commands I used were:

```
python collect_keyword.py 2794 omics
python collect_keyword.py 2794 metagenomics
python collect_keyword.py 2794 rnaseq
python collect_keyword.py 2794 bioinformatics
```

---
