# Research and Patent Landscape Informatics

Computational approaches to exploring research, funding, patent, and innovation landscapes.

## Overview

This workshop series introduces computational approaches to research and patent landscape analysis. The workshops explore several major sources of scholarly and patent information and demonstrate how Python, APIs, SQL, network analysis, and local generative AI can be used to investigate research and innovation.

Research and patent landscapes can bring together many kinds of information. Scholarly databases provide information on publications, patents, researchers, institutions, citations, and research topics. Rather than focusing on a single database or a single approach to analyzing research and innovation data, this series examines several different information systems and the relationships among the data they contain.

Each workshops begins with data access. Participants use OpenAlex, Dimensions, the USPTO Open Data Portal, Google Patents, and Google BigQuery to search for and retrieve information about publications, grants, patents, researchers, and inventors. Examples move from web interfaces to APIs and SQL so that participants can see both how these systems are searched interactively and how their underlying data can be investigated computationally.

Later projects build on these data-access skills, including summarization, classification, and network analysis of interconnected publications and patents. A final capstone combines USPTO Patent File Wrapper data with locally running AI models through Ollama to extract patent text, summarize an invention, interpret patent drawings, and experiment with prior-art relevance screening.

The examples are deliberately introductory. They are intended to provide enough experience with each system and method for participants to begin adapting the workflows to their own research questions rather than providing complete or automated data analytics pipeline.

An important goal of the series is not simply to learn a particular set of databases. It is to develop a transferable approach to working with research information:

1. Understand the information source and how it represents research or innovation
2. Search the system through its user interface
3. Retrieve and inspect the underlying data
4. Organize and analyze the data computationally
5. Evaluate the limitations of the source and the methods being used
6. Adapt the workflow to a new research question

Research and patent landscape analysis frequently involves incomplete metadata, ambiguous identities, different classification systems, changing terminology, and information distributed across multiple databases. These workshops introduce tools for investigating those problems while leaving the more difficult work of defining a research question, evaluating evidence, and combining information sources to the researcher.

## Table of Contents

- [Objectives](#objectives)
- [Prerequisites](#prerequisites)
- [Approach](#approach)
- [Data Sources](#data-sources)
  - [OpenAlex](#openalex)
  - [Dimensions](#dimensions)
  - [USPTO](#uspto)
  - [Google Patents and BigQuery](#google-patents-and-bigquery)
- [Workbooks](#workbooks)
  - [OpenAlex Workbooks](#openalex-workbooks)
  - [Dimensions Workbooks](#dimensions-workbooks)
  - [USPTO Workbooks](#uspto-workbooks)
  - [Google Patents and BigQuery Workbook](#google-patents-and-bigquery-workbook)
  - [Network Project Workbooks](#network-project-workbooks)
  - [Local AI Patent Analysis Workbook](#local-ai-patent-analysis-workbook)
- [Exploring Your Own Research Questions](#exploring-your-own-research-questions)
- [Relationship to the Workshop Series](#relationship-to-the-workshop-series)
- [Reading and Research Resources](#reading-and-research-resources)
  - [Patents and Research](#patents-and-research)
  - [Research and Patent Information Systems](#research-and-patent-information-systems)
  - [Sample Patent Landscape Reports](#sample-patent-landscape-reports)
  - [Patent and Intellectual Property Research Guides](#patent-and-intellectual-property-research-guides)
  - [AI and Patentable Research](#ai-and-patentable-research)
- [Instructor](#instructor)
- [Additional Resources](#additional-resources)
- [Citation](#citation)

## Objectives

By the end of this workshop series, participants will be able to:

- Identify several major sources of research and patent information
- Search research and patent databases through their web interfaces
- Retrieve research and patent data programmatically using APIs
- Work with JSON returned by web APIs
- Organize and build small research datasets using pandas
- Use SQL to query large public patent datasets
- Construct simple researcher and inventor collaboration networks
- Apply locally running AI models to patent documents and drawings
- Adapt example queries and workflows to investigate research and technology areas of interest

## Prerequisites

This series builds on the UCSF Library's broader curriculum in computational data and document analysis.

Participants should have some previous experience with:

- Unix
- Python
- pandas
- APIs and JSON
- SQL
- basic data visualization

The workshops use these technologies to investigate research and patent information rather than teaching each technology from the beginning.

Some workshops require access to particular databases or services. Participants are not expected to have prior experience with these databases. Setup and access requirements are described with the individual workshop materials.

## Approach

The data-access workshops follow a consistent pattern.

We begin with the web interface or search system so that we can understand the information source itself. We then retrieve information programmatically and inspect the data returned by the system.

A typical workshop moves through:

1. Search or explore the information source through the web based User Interface
2. Search the information source using Python based API access
3. Inspect JSON or other structured data
4. Organize results in a pandas DataFrame
5. Create a simple visualization or analysis
6. Modify the example to investigate another topic

The goal is not to provide an exhaustive introduction to every database. Instead, the workshops provide enough experience with several different systems for participants to begin adapting the methods to their own research questions.

The later projects build on these data-access skills by using retrieved data for network analysis and local AI workflows.

## Data Sources

### OpenAlex

[OpenAlex](https://openalex.org/) is an open catalog of scholarly research information containing publications, authors, institutions, topics, citations, and related metadata.

OpenAlex provides a relatively accessible introduction to research information APIs. Basic access does not require participants to create an API key.

### Dimensions

[Dimensions](https://www.dimensions.ai/) integrates information about publications, grants, patents, researchers, organizations, and other research outputs.

The Dimensions API uses the Dimensions Search Language (DSL) to query these records and the relationships among them.

Dimensions access depends on institutional permissions and API availability.

### USPTO

The [USPTO Open Data Portal](https://data.uspto.gov/) provides programmatic access to patent application information and Patent File Wrapper data.

The workshops use the USPTO API to work with structured patent metadata as well as the underlying documents associated with patent applications.

USPTO Open Data Portal access requires an API key. To generate a key, you must create a public account, but no special institutional access is required. 

### Google Patents and BigQuery

[Google Patents](https://patents.google.com/) provides a web interface for searching and exploring patents from multiple patent offices.

Google also makes large patent datasets available through [Google BigQuery](https://cloud.google.com/bigquery), allowing patent data to be queried using SQL.

Together, these resources provide an opportunity to move between interactive patent searching, individual patent records, and large-scale computational queries.

Access to BigQuery is available through the sandbox for anyone with a google account (email, drive). No payment method is required to query google public data sources (including publications and patents) through the sandbox. Paid tiers will provide better performance and higher memory limits but are not required for this workshop. 

## Workbooks

The notebooks and workshop materials in this repository progress from introductory data access to small applied projects.

Participants are encouraged to modify the examples and investigate researchers, inventors, technologies, grants, and research areas related to their own interests.

### OpenAlex Workbooks

#### [OpenAlex-API-Introduction.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/OpenAlex-API-Introduction.ipynb)

This workbook introduces the OpenAlex API using scholarly publication data.

The example begins with a single known publication and examines the JSON returned by OpenAlex. It then searches for publications related to a research topic, selects useful fields, creates a pandas DataFrame, and produces a simple visualization.

The workbook introduces the general pattern used throughout the series: retrieve data, inspect the response, organize the results, and modify the search to investigate another question.

#### [OpenAlex-Coauthor-Network.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/OpenAlex-Coauthor-Network.ipynb)

This project uses OpenAlex publication data to construct a researcher collaboration network.

Starting with one researcher, the notebook retrieves recent publications, identifies coauthors, and expands outward through the collaboration network. Researchers become nodes, while shared publications create weighted edges between researchers.

The resulting network is constructed and visualized using NetworkX.

### Dimensions Workbooks

#### [Dimensions-API-Introduction.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/Dimensions-API-Introduction.ipynb)

This workbook introduces the Dimensions API and Dimensions Search Language (DSL).

The example retrieves a small set of publications, inspects the returned records, searches publications for a research topic, selects useful fields, creates a pandas DataFrame, and produces a simple visualization.

Dimensions API access requires an institutional account with API permissions.

#### [Dimensions-Grant-to-Patents.ipynb](Dimensions-Grant-to-Patents.ipynb)

This workbook explores relationships between research funding and patent activity.

Starting with a research area, the notebook searches Dimensions for grants associated with the University of California, San Francisco. It then uses the Dimensions grant IDs to find patent records associated with those grants.

The example demonstrates how classifications, identifiers, and relationships in a research information system can be used to move between different kinds of records and investigate connections between research funding and innovation.

### USPTO Workbooks

#### [USPTO-API-Introduction.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/USPTO-API-Introduction.ipynb)

This workbook introduces the USPTO Patent File Wrapper API.

The example retrieves a single known patent application, examines the JSON returned by the API, searches patent application data using a technology term, creates a pandas DataFrame, and examines Cooperative Patent Classification (CPC) codes.

USPTO Open Data Portal access requires an API key.

#### [USPTO-File-Wrapper-Drawings.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/USPTO-File-Wrapper-Drawings.ipynb)

This workbook moves from structured patent metadata to the documents contained in a patent application's file wrapper.

Starting with an application number, the notebook retrieves the available file-wrapper documents, organizes them in a pandas DataFrame, identifies drawing documents, downloads a drawing PDF, and renders pages as images.

The example provides a bridge between patent metadata and the underlying patent documents.

#### [USPTO-CoInventor-Network.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/USPTO-CoInventor-Network.ipynb)

This project constructs an inventor collaboration network from USPTO patent application data.

Starting with one inventor, the notebook retrieves patent applications, identifies co-inventors, and expands outward through the collaboration network.

Inventors become nodes, while appearing together on a patent application creates weighted edges. The resulting network is constructed and visualized using NetworkX.

### Google Patents and BigQuery Workbook

#### [GoogleBigQuery.md](GoogleBigQuery.md)

This workshop introduces Google Patents and the Google Patents Public Datasets in BigQuery.

Participants begin with the Google Patents web interface to search for patents and examine individual records. The workshop then moves to BigQuery, where SQL is used to inspect the patent dataset schema, search for inventors and technologies, retrieve known patents, explore CPC classifications, and move between BigQuery records and individual patents in Google Patents.

The examples are intended to be modified to investigate technologies, inventors, organizations, patent classifications, and research areas of interest.

### Network Project Workbooks

This workshop uses researcher and innovator data from OpenAlex and the USPTO Open Data Portal to construct and visualize innovation networks. 

The two network notebooks are intentionally parallel applications of the same general idea.

[OpenAlex-Coauthor-Network.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/OpenAlex-Coauthor-Network.ipynb) constructs a researcher collaboration network from publication authorship.

[USPTO-CoInventor-Network.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/USPTO-CoInventor-Network.ipynb) constructs an inventor collaboration network from patent inventorship.

### Local AI Patent Analysis Workbook

#### [USPTO-Ollama-Patent-Analysis.ipynb](https://github.com/UCSF-DSOS/Research-Patent-Landscape-Informatics/blob/main/USPTO-Ollama-Patent-Analysis.ipynb)

This capstone combines USPTO data retrieval with locally running generative AI models through [Ollama](https://ollama.com/).

Starting with a patent application, the notebook retrieves Patent File Wrapper documents and creates a small analysis pipeline:

1. Download a patent specification
2. Render patent pages as images
3. Use DeepSeek-OCR to extract text
4. Use Gemma 3 to summarize the patent
5. Retrieve and render a patent drawing
6. Use Qwen3-VL to describe the drawing
7. Use Strands Decider to estimate whether the patent is relevant to a user-defined prior-art search topic

Different models are used for different tasks rather than treating a single generative AI model as a universal analytical tool.

The relevance classification is intended as a screening and research exercise. Model-generated scores are not legal determinations regarding prior art, novelty, obviousness, infringement, or patentability.

For a broader introduction to locally running generative AI models, model selection, OCR, image analysis, classification, and document-based chat, see:

[Local AI with Ollama](https://ucsf-dsos.github.io/Local-AI-With-Ollama/)

## Exploring Your Own Research Questions

The examples in this repository are intended to be modified.

Participants are encouraged to investigate:

- researchers
- inventors
- technologies
- research topics
- organizations
- grants and funding
- patent classifications
- research collaborations
- inventor collaborations
- relationships between research and innovation

As the series progresses, participants should increasingly be able to adapt the examples to new databases and information systems rather than relying on a prepared notebook for every source.

Research and patent landscape analysis often requires combining multiple sources, evaluating incomplete or inconsistent metadata, resolving identities, refining search strategies, and deciding what relationships are meaningful for a particular research question.

Those challenges are part of the research process rather than problems that these introductory notebooks attempt to solve automatically.

## Relationship to the Workshop Series

This workshop series builds on the UCSF Library curriculum in computational data and document analysis with Python, SQL, machine learning, and AI.

The broader workshop series introduces foundational methods including:

- Python and pandas
- SQL
- APIs and JSON
- data visualization
- text and document analysis
- network analysis
- machine learning
- OCR and transcription
- local generative AI

This repository applies those methods specifically to research and patent information.

Related workshop materials include:

- [Local AI with Ollama](https://ucsf-dsos.github.io/Local-AI-With-Ollama/)
- UCSF Library workshops on Python, SQL, APIs, data visualization, machine learning, and document analysis

## Reading and Research Resources

### Patents and Research

Patent landscape analysis can be used to investigate technology development, research activity, innovation, and relationships between scientific research and patenting.

Some starting points include:

- [Are university policies holding science back? Study shows how patenting boosts pure research](https://newsroom.haas.berkeley.edu/research/are-university-policies-holding-science-back-study-shows-how-patenting-boosts-pure-research/)
- [Patent landscape analysis—Contributing to the identification of technology trends and informing research and innovation funding policy](https://pmc.ncbi.nlm.nih.gov/articles/PMC10034625/)
- [Patent Leaderboard](https://www.patentleaderboard.com/patents/most-valuable)

For additional examples, search PubMed for `"patent landscape"` and identify landscape studies related to a research area that interests you:

[PubMed](https://pubmed.ncbi.nlm.nih.gov/)

These studies can provide examples of research questions, search strategies, classification approaches, visualizations, and methods used in published patent landscape analyses.

### Research and Patent Information Systems

- [OpenAlex](https://openalex.org/)
- [Dimensions](https://www.dimensions.ai/)
- [USPTO Patent Public Search](https://www.uspto.gov/patents/search/patent-public-search)
- [USPTO Open Data Portal](https://data.uspto.gov/)
- [Google Patents](https://patents.google.com/)
- [The Lens](https://www.lens.org/)
- [Web of Science](https://www.webofscience.com/)
- [Derwent Innovations Index](https://clarivate.com/academia-government/scientific-and-academic-research/research-discovery-and-referencing/web-of-science/derwent-innovations-index/)

Web of Science can provide information about patents that cite scholarly publications when available. Derwent Innovations Index provides dedicated patent-search capabilities.

These systems are included as resources even when they are not the subject of a prepared workshop notebook. One goal of the series is to develop skills that can be transferred to additional research and patent information systems.

### Sample Patent Landscape Reports

The World Intellectual Property Organization publishes patent landscape reports covering a variety of technologies and policy questions:

[WIPO Patent Landscape Reports](https://www.wipo.int/publications/en/series/index.jsp?id=137)

One example:

[Decarbonizing Heavy Duty Road Transport — Digitalization, Fleet and Operations Management](https://www.wipo.int/web-publications/patent-landscape-report-decarbonizing-heavy-duty-road-transport/en/6-digitalization-fleet-and-operations-management.html)

### Patent and Intellectual Property Research Guides

University of California resources:

- [UC San Diego Patents Guide](https://ucsd.libguides.com/patents/)
- [UC Irvine Patents and Trademarks](https://guides.lib.uci.edu/patents-and-trademarks/)
- [UC Santa Barbara Patents Guide](https://guides.library.ucsb.edu/patents)
- [UC Merced Patents and Trademarks](https://libguides.ucmerced.edu/patents_and_trademarks)
- [UC Berkeley Patents Guide](https://guides.lib.berkeley.edu/patents)
- [UCLA Materials Science Patent Resources](https://guides.library.ucla.edu/c.php?g=180271&p=1190819)
- [UC Davis Drug Discovery, Development and Commercialization](https://guides.library.ucdavis.edu/drug-development/patents)
- [UC Riverside Patents and Trademarks Collection](https://library.ucr.edu/collections/patents-trademarks-collection)
- [UC Santa Cruz Electrical and Computer Engineering Patent Resources](https://guides.library.ucsc.edu/c.php?g=119678&p=9150279)

Additional guides:

- [Georgia Tech Patent Landscape Analysis](https://libguides.library.gatech.edu/c.php?g=1240806&p=9204744)
- [University of Arizona Intellectual Property and Patent Landscapes](https://libguides.library.arizona.edu/ipp/landscapes)
- [Queen's University Patents Guide](https://guides.library.queensu.ca/patents/patents-home)

### AI and Patentable Research

For an example of institutional guidance concerning generative AI and patentable work:

[UC San Diego — AI and Intellectual Property](https://innovation.ucsd.edu/disclose-patent/ai-and-intellectual-property.html)

## Instructor

Geoffrey Boushey is a computational and research data science specialist at UCSF and a member of the Library's Data Science and Open Scholarship team.

Geoff teaches courses and provides consultations on foundational programming, data analysis, and AI techniques including Python, SQL, Unix, version control, machine learning, and generative AI.

## Additional Resources

- [OpenAlex](https://openalex.org/)
- [Dimensions](https://www.dimensions.ai/)
- [USPTO](https://www.uspto.gov/)
- [USPTO Open Data Portal](https://data.uspto.gov/)
- [Google Patents](https://patents.google.com/)
- [Google BigQuery](https://cloud.google.com/bigquery)
- [The Lens](https://www.lens.org/)
- [Ollama](https://ollama.com/)
- [Local AI with Ollama](https://ucsf-dsos.github.io/Local-AI-With-Ollama/)
- [WIPO](https://www.wipo.int/)

## Citation

If you use this curriculum, code, or these workshop materials in your research or teaching, please cite them using `CITATION.cff` or as follows:

**APA:**

> Boushey, G. (2026). *Research and Patent Landscape Informatics* (Version 1.0.0) [Computer software]. UCSF Library. https://github.com/UCSF-DSOS/Research-Patent-Landscape-Workshop

**BibTeX:**

```bibtex
@software{Boushey_Research_Patent_Landscape_Informatics_2026,
  author    = {Boushey, Geoffrey},
  title     = {Research and Patent Landscape Informatics},
  url       = {https://github.com/UCSF-DSOS/Research-Patent-Landscape-Workshop},
  version   = {1.0.0},
  year      = {2026},
  publisher = {UCSF Library}
}
```
