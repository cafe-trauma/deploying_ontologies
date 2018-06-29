# Deploying Ontologies using Github and the Obofoundry
This is a guide for deploying your ontologies to be hosted on github and using the [Obofoundry](http://www.obofoundry.org/) for purls.
Our goal is to have seperate URIs for development, individual releases, and the most up to date release version; all without needing to edit configuration files for each release.

## Initial setup
* Create a github repo for your ontology.
* Fork the purl.obolibrary.org repository using [these instructions](https://github.com/OBOFoundry/purl.obolibrary.org)
* Create a new config file in the forked repository using these settings, except modified to your ontology/github repo.

```
# PURL configuration for http://purl.obolibrary.org/obo/example

idspace: EXAMPLE
base_url: /obo/example

products:
- example.owl: https://raw.githubusercontent.com/EXAMPLE/EXAMPLE/master/example.owl

term_browser: ontobee
example_terms:
- EXAMPLE_00000029

entries:
- prefix: /release/
  replacement: https://raw.githubusercontent.com/EXAMPLE/EXAMPLE/
  
- exact: /dev/example.owl
  replacement: https://raw.githubusercontent.com/EXAMPLE/EXAMPLE/master/development/example.owl
```
* Move your current working version of your owl file into a development directory in your github repo directory.
* Change the ontology URI of your development version ontology to `http://purl.obolibrary.org/obo/YOUR_ONTOLOGY/dev/your_ontology.owl`.
* Push these changes to github and make a pull request for the purl.obolibrary.org repository.

Wait a few minutes and ensure that the above link resolves properly to your development ontology.

## Creating releases
* `Save as...` your development ontology into the base level of your github repo directory, keep the name the same.
Now your directory structure should look like.
```
.
├── example.owl
├── README.md
├── development
│   └── example.owl
```
Ensure you are currently editing the OWL file in the base directory, this will be the release version.
* Set the Ontology IRI to `http://purl.obolibrary.org/obo/YOUR_ONTOLOGY/your_ontology.owl`.
* Set the Ontology Version IRI to `http://purl.obolibrary.org/obo/YOUR_ONTOLOGY/release/RELEASE_NAME/your_ontology.owl`.
* Create a git tag for your RELEASE name and push it.
`git tag RELEASE_NAME`
`git push --tags`
Your release and version should now be routing properly using their IRIs.
