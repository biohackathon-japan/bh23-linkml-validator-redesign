---
title: 'BioHackJP 2023 Report R4: Redesign of the validation framework in LinkML'
title_short: 'BioHackJP 2023 LinkML Validator Redesign'
tags:
  - Linked Data
  - Link modeling language
  - Validation
authors:
  - name: Deepak R. Unni
    orcid: 0000-0002-3583-7340
    affiliation: 1
  - name: Andra Waagmeester
    orcid: 0000-0001-9773-4008
    affiliation: 2
  - name: Jose Emilio Labra Gayo
    orcid: 0000-0001-8907-5348
    affiliation: 3
affiliations:
  - name: SIB Swiss Institute of Bioinformatics, Switzerland
    index: 1
  - name: Second Affiliation
    index: 2
  - name: Third Affiliation
    index: 3
date: 30 June 2023
cito-bibliography: paper.bib
event: BH23JP
biohackathon_name: "BioHackathon Japan 2023"
biohackathon_url:   "https://2023.biohackathon.org/"
biohackathon_location: "Kagawa, Japan, 2023"
group: R4
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/biohackathon-japan/bh23-linkml-validator-redesign
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Deepak R. Unni \emph{et al.}
---

# Background

LinkML is a data modeling language that can be used to describe the structure and semantics of data from a specific domain. LinkML lets you manage various levels of semantic expressivity, depending on the use-case at hand. As a result, data models expressed in LinkML can be utilized with various (relational and non-relational) data stores.

There are two parts to the LinkML ecosystem:
- **the modeling language:** a vocabulary that can be used to define data models
- **the tooling:** a suite of tools for generating technology-specific artifacts from data models

As with any data ecosystem, there ixs also a need for tools that support validation of data. Currently, the LinkML ecosystem provides a simple validation utility that can be used to validate data against a LinkML schema. But this validation utility makes use of JSON Schema for validating data. While this does cover several validation use-cases, it is still limited in its applicability and scope. Thus, there is a need for a data validation utility that is flexible and can grow organically according to use-cases.

The goal of this project was to improve on LinkML's validation framework by adopting certain design principles:

1. **Schema Agnostic:** The validator must be schema agnostic and must not make any assumptions on the incoming data outside of the scope of LinkML metamodel (i.e. the validator should run for any given LinkML schema).
2. **Plugin Architecture:** Each type of validation should be its own plugin. This ensures that validation scenarios are atomic, well documented, and can be configured for appropriate use-cases. Plugins can be internal or external, with both types supported.
3. **Extendable Parsers**: The validator should be able parse various types of data formats and data stores and should be configurable such that the choice of the validator is left to the user with sensible defaults applied where required.
4. **Easy to Configure:** The plugins, and by extension, the validator should be configurable at runtime such that the plugin and validator behavior can be tweaked for certain inputs or use-cases.
5. **Parseable Validation Messages:** The validator should return validation results and reports that are concise, easy to parse, and conforms to a well defined structure. Since the validation framework is aware of the LinkML metamodel, it can also make use of the native LinkML validation schema to ensure that the structure of the validation reports are aligned and compatible with the LinkML ecosystem.

Following the aforementioned design principles will ensure flexibility and sustainability of the validation tool. 

# Outcomes

## Redesign of the Validation

We approach the redesign of the existing LinkML validation tool by implementing the following components:
- Models
- Loader
- Validation Plugins
- Validator


### Models

A set of well defined validation classes that serve as the structure of the validation response

### Loader

For parsing input data and getting it to a state that can then be used by the validation plugins

### Validation Plugins

A plugin that is responsible for running a set of operations on a given input data and is aware of the provided schema

### Validator

A common validation interface for invoking the validator with a given schema, a set of input data and validation plugins


![Design](./design.png)



![Caption for BioHackrXiv logo figure](./biohackrxiv.png)

# Future work

Moving forward, there are several areas of potential future work to enhance our project's linked data standardization with LLMs. First, exploring advanced LLMs and optimizing computational efficiency can improve performance. Additionally, expanding ontology mapping to cover more domains and integrating external data sources would increase the scope of our standardization efforts. Validating and evaluating results against gold-standard datasets, involving domain experts, and developing a user-friendly interface for researchers to interact with the pipelines are crucial next steps. These future endeavors will refine and advance our methodology, increasing its impact and adoption in bioinformatics.


# Discussion

A flexible framework for performing validation of data against any given LinkML-based schema can have a positive impact on the LinkML community. New (and existing users) can adopt the validation framework and extend it for their needs to ensure data quality, data consistency, and also perform checks that may not be possible (or easy) in the context of Pydantic, JSONSchema, or Shape Expressions. The work highlighted can serve as a useful utility for data integration and validation pipelines that need a reliable way to identify data inconsistencies and report them in a way that is actionable. The work outlined is an addition to the rapidly developing LinkML ecosystem and collectively aims to make schema representation, data representation, and data harmonization easier and manageable - especially in the context of biological and biomedical data.

## Acknowledgements

We would like to thank the fellow participants at BioHackathon 2023 for their collaboration and constructive advice, which greatly influenced our project. We are grateful to the organizers for providing this platform and the developers of open source language models. We are also grateful to the LinkML developers and the wider community for being active, engaged, and constructive with their requirements and feedback.

## References

1.
