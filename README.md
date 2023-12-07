# wikipedia-dump

Extracts text data from wikipedia dumps.



# Dependencies

[Wikiextractor](https://github.com/attardi/wikiextractor)



# Running the project

## Create a virtual environment

```shell
python3 -m venv venv
```

## Activate the virtual environment

```shell
source venv/bin/activate
```

## Install the dependencies 

```shell
pip install -r requirements.txt
```



# Wikipedia Dumps

Download the latest portuguese dump into the data folder:

```bash
curl https://dumps.wikimedia.org/ptwiki/latest/ptwiki-latest-pages-articles-multistream-index.txt.bz2 --create-dirs -o data/ptwiki-latest-pages-articles-multistream-index.txt.bz2
```

```bash
curl https://dumps.wikimedia.org/ptwiki/latest/ptwiki-latest-pages-articles-multistream.xml.bz2 --create-dirs -o data/ptwiki-latest-pages-articles-multistream.xml.bz2
```

Unzip the file

```bash
bzip2 -dk data/ptwiki-latest-pages-articles-multistream-index.txt.bz2
```

```bash
bzip2 -dk data/ptwiki-latest-pages-articles-multistream.txt.bz2
```

The latest dump can be found in the file:
[ptwiki-latest-pages-articles-multistream.xml](./data/ptwiki-20231020-pages-articles-multistream.xml)

The articles index can be found in the index file: 
[ptwiki-latest-pages-articles-multistream-index.txt](./data/ptwiki-20231020-pages-articles-multistream-index.txt)



# How to get only the __text__ data from the XML dump file?

Wikipedia allow us to download all articles data, but it's in XML format.

The XML file is more the 9GB large, so it's necessary to find a way to open it without using the whole memory.

## Wikiextractor

```shell
 wikiextractor --no-templates -o data/ptwiki-latest-pages-articles-multistream-processed/ -b 100M \
 --json \
 data/ptwiki-latest-pages-articles-multistream.xml.bz2
```

## GitHub repo where I have found Wikiextractor

pt-BR Corpus with the Wikipedia dump.

[PT BR Corpus](https://github.com/eberlitz/pt-br-corpus).



# Alternative Strategy

Split the file. To do that we can use a shell command:

```shell
split -b 50MB data/ptwiki-latest-pages-articles-multistream-index.txt
```

```shell
split -b 1GB data/ptwiki-latest-pages-articles-multistream.xml
```
