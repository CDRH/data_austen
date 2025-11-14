# Data Repository for Austen Said: Patterns of Diction in Jane Austen's Major Novels

## About This Data Repository

**How to Use This Repository:** This repository is intended to be used with the [Austen Said Ruby on Rails application](https://github.com/CDRH/austen). This repository is not intended for use with the CDRH API.

**Data Repo:** [https://github.com/CDRH/data_austen](https://github.com/CDRH/data_austen)

**Source Files:** TEI XML

**Script Languages:** Ruby, XSLT, JavaScript

**Encoding Schema:** [Text Encoding Initiative (TEI) Guidelines](https://tei-c.org/release/doc/tei-p5-doc/en/html/index.html)

## About Austen Said: Patterns of Diction in Jane Austen's Major Novels

This site allows you to explore Austen's patterns of diction. We feature word frequencies, a search, novel visualizations, and background on the project.

**Project Site:** [https://austen.unl.edu/](https://austen.unl.edu/)

**Rails Repo:** [https://github.com/CDRH/austen](https://github.com/CDRH/austen)

**Credits:** [https://austen.unl.edu/about#team](https://austen.unl.edu/about#team)

## Conditions of Use

Created by the Center for Digital Research in the Humanities.

## Technical Information

- Framework: Ruby on Rails
- Search and Browse functionality: Apache Solr
- Data Querying and Transformation: XSLT Scripts (powered by Saxon 9 HE)
- Data Indexing: Ruby Scripts

See the project site's [Technical Information](https://austen.unl.edu/about#technical) section for more information.

## About the Center for Digital Research in the Humanities

The Center for Digital Research in the Humanities (CDRH) is a joint initiative of the University of Nebraska-Lincoln Libraries and the College of Arts & Sciences. The Center for Digital Research in the Humanities is a community of researchers collaborating to build digital content and systems in order to generate and express knowledge of the humanities. We mentor emerging voices and advance digital futures for all.

**Center for Digital Research in the Humanities GitHub:** [https://github.com/CDRH](https://github.com/CDRH)

**Center for Digital Research in the Humanities Website:** [https://cdrh.unl.edu/](https://cdrh.unl.edu/)

## Index Data in Solr

To index this repo's data in Solr, we first need to upload the Solr 9 compatible
API configset to Solr's `/var/local/solr-data/data/` subdirectory.

```bash
rsync -ahuX config/solr/data/configsets user@server.unl.edu:

# Then SSH into the server and move the files into place with root permissions
# and set solr as the owner
sudo mv /home/(user)/configsets /var/local/solr-data/data/
sudo chown -R solr:solr /var/local/solr-data/data/configsets
```

Now we should be able to run the Datura commmands from this repository to create
the core and set the schema for Austen's data. Lastly, post the data.

```bash
solr_create_api_core austen

solr_manage_schema -o true -j config/schema.json

post -x solr
```

These commands use development environment config by default.
Add `-e production` option to run the commands in production environments
