# KALI Dumps scripts

[![Build Status](https://travis-ci.com/SocialGouv/kali_dumps_scripts.svg?branch=master)](https://travis-ci.com/SocialGouv/kali_dumps_scripts)

These tools help using KALI dumps (the French Conventions collectives nationales database).

This project was created for the [Code Du Travail Numérique](https://incubateur.social.gouv.fr/startups/code-du-travail-numerique/) project.

The app is divided into 3 separate docker containers:

- **api**: a lightweight read-only REST API that exposes the MongoDB collections (with HATEOAS).
- **mongodb**: a MongoDB server that stores the parsed documents
- **extractor**: Python scripts to download, extract, parse the XMLs and insert them into MongoDB.

Additionally, the scripts let you:
- flatten all nested XML documents to a common directory
- convert all the articles' XML files to individual JSON files

## Coming soon

We're working on publishing a public version of this MongoDB database and of the JSON REST API.

## Schema docs

You can find some work-in-progress docs on a [Google Spreadsheet here](https://github.com/SocialGouv/kali_dumps_scripts.git).

![docs screenshot](https://i.imgur.com/8XgOmhL.png)

The infos in this documentation come from:
- the DTD files available on Data Gouv
- exploring the MongoDB database that these scripts help create. The M3T tool is very helpful for this.

## Local setup

This should start the MongoDB server and the Python's Eve API.

```sh
docker-compose up
```

Then you have to run a script from the `kali_extractor` container to fetch, parse and store into MongoDB the KALI dumps.

```sh
docker-compose run extractor python parser.py --download
```

## Usage

The REST API is accessible locally on [http://localhost:5000](http://localhost:5000). Use `curl` or `httpie` to access it, by default it will return XML to browsers which is not very convenient.

The MongoDB database is exposed on your host machine on port 27019 with the `kali:kali` credentials on the `admin` db.

You can access it using any MongoDB client (I recommend [Studio 3T](https://studio3t.com/download/)) to explore.


## External Resources

- [original KALI dumps on Data Gouv](https://www.data.gouv.fr/fr/datasets/kali-conventions-collectives-nationales/)
- sample "convention collective" [on Legifrance](https://www.legifrance.gouv.fr/affichIDCC.do;jsessionid=345B979AD534CB99791356E28B8A9CB0.tplgfr35s_1?idSectionTA=KALISCTA000005733781&cidTexte=KALITEXT000005639851&idConvention=KALICONT000005635890)
- [Code Du Travail Numérique](https://incubateur.social.gouv.fr/startups/code-du-travail-numerique/) project.
