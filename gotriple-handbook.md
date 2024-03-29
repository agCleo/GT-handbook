
***WORK IN PROGRESS***
-----

# GoTriple Content Providers Handbook

## Purpose of this document
[GoTriple](https://www.gotriple.eu/) is a discovery service for the Social Sciences and Humanities community. It is one of the services of the European Research Infrastructure [OPERAS](https://www.operas-eu.org/).   
The GoTriple platform allows to search through publications, datasets, researchers' profiles, and research projects. Publications and datasets metadata are collected from both content aggregators and content providers (see [Glossary](#glossary)).

This handbook is addressed to the **GoTriple content providers**. 
It presents the policies, technical requirements, and supporting actions enabling the providers' content acquisition and processing by the GoTriple platform. It informs them as well about other aggregators' policies.

## GoTriple Policies
### Scope
*Scientific fields*: GoTriple collects metadata of contents in the **Social Sciences and Humanities (SSH)** field. The content providers can be domain specific or not.

*Data definition*: GoTriple only collects **metadata of the contents**. The platform does not collect or store the contents of the providers.

*Geographic area*: GoTriple operates in the **European area** and collects data from European providers. The platform provides enrichments for a limited number of European languages and  collects therefore contents firstly in these languages.

*Openness*: As a service of OPERAS, the RI dedicated to open scholarly communication in the SSH, GoTriple supports **open access** to the contents. The platform however collects open and not open access contents. The metadata of the contents need to be freely accessible and reusable.

*Providers type*: GoTriple providers can be of any size and provide large or small amount of contents in one or many SSH fields. GoTriple works with major aggregators, but also facilitates data acquisition from **small repositories or publishers**, like for instance diamond journals.

*GoTriple supported languages*: Croatian, English, French, German, Greek, Italian, Polish, Portuguese, Spanish. 

### Content types
This handbook only considers the data collected about scientific resources. Data about researchers' profiles and research projects are collected through distinct automated processes.   
In GoTriple, the resources are publications and datasets, which are all named "documents".  A **document** is the information asset of a unique and deduplicated resource.

The list of content types available on GoTriple is based on a subset of the [COAR](https://vocabularies.coar-repositories.org/resource_types/) list of types (see [Annexe](#gotriple-list-of-content-types)).   
On GoTriple, **publications** are any type of text or material related to the SSH research environment, from articles or thesis, to reports or learning material. 
As for the **datasets**, they are a set of organized research data. In the context of GoTriple, these resources are only indexed at the level of the global collection. Each single file of the datasets is therefore not indexed.   

## GoTriple Requirements
In order to have their contents collected by GoTriple, the providers essentially have to respect two requirements: providing an *access to their metadata*; providing *metadata compliant* with the platform's data model.   
The following two sections specify the technical set-up enabling GoTriple to access the metadata and the model that these metadata should follow to be indexed by GoTriple.

### Technical set-up
GoTriple collects data from the content providers by using the Open Archive Initiative - Protocol for Metadata Harvesting ([OAI-PMH](http://www.openarchives.org/OAI/openarchivesprotocol.html)). Metadata compliant with the protocol can also be collected as a dump, without an OAI repository. This solution however hinders automated data acquisition and updates. Using a repository harvestable through OAI-PMH should therefore be preferred.
   
The OAI-PMH protocol was developed in 1999 as part of the Open Archives Initiative. It allows content providers to expose their metadata on the Web in a structured format and to make it available for harvesters. The repository is set-up by the provider and contains sets of metadata. The metadata has to be represented according to the [simple DublinCore (DC)](https://www.dublincore.org/specifications/dublin-core/dces/) standard at least, or in a more expressive format, like for instance [qualified DublinCore (QDC)](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/). DC and QDC can be expressed in XML, HTML, or XHTML files. The OAI-PMH allows harvesters like GoTriple to then collect the structured metadata.   
The OAI repository can be set up by the content provider with little development investment. Some tools and services for data repositories or publishers can contain an OAI-PMH module, either as a built-in feature or a plugin (e.g. [DSpace](https://duraspace.org/dspace/resources/technical-specifications/), [OJS](https://docs.pkp.sfu.ca/learning-ojs/en/settings-distribution#access)).

### GoTriple data model
In order to ensure high semantic expressivity and address flexibility needs, the TRIPLE data model is based on the [schema.org](https://schema.org/) ontology, which is maintained by a [World Wide Web Consortium (W3C) community](https://www.w3.org/community/schemaorg/). The ontology allows to handle the metadata of documents, but also of profiles and projects. The metadata of the documents need to be compliant with DublinCore. Thanks to various mappings between metadata standards, the TRIPLE data model can handle other major standards well-spread in the SSH community, like OpenAIRE metadata format or Europeana Data Metadata (EDM) format.

Below, we describe the current TRIPLE data model for documents, specifying the level of priority, the corresponding tag elements in simple DC and QDC, and their expression in the TRIPLE data model.  
   
   
| Priority | Description | DublinCore | Triple data model | 
| :---     |    :----:   | :---:      | :----: | 
| Mandatory | Creator of the resource| dcterms:creator, dc:creator| schema:author |
| Mandatory | Identifier of the resource| dcterms:identifier, dc:identifier | schema:identifier |
| Mandatory | Title of the resource| dcterms:title, dc:title| schema:headline |
| Recommended | Abstract  | dcterms:description, dc:description, dcterms:abstract | schema:abstract |
| Recommended | Access rights to the resource | dcterms:accessRights, dcterms:conditions??, dc:conditions?? |schema:conditionsOfAccess |
| Recommended | Date of publication or creation  | dcterms:date, dc:date, dcterms:issued, dcterms:created, dcterms:available | schema:datePublished |
| Recommended | Keywords  | dcterms:subject, dc:subject | schema:keywords |
| Recommended | Language of the resource | dcterms:language, dc:language | schema:inLanguage | 
| Recommended | License | dcterms:rights, dc:rights | schema:license |
| Recommended | Publisher of the resource | dcterms:publisher, dc:publisher | schema:publisher |
| Recommended | URL of the landing page | dcterms:identifier  dc:identifier | schema:mainEntityOfPage |
| Recommended | URL of the resource | dcterms:identifier  dc:identifier | schema:url |
| Recommended | URL of the source (e.g. URL of a publishing platform) | dcterms:source, dc:source | schema:isBasedOnURL |
| Optional | Type of the resource | dcterms:type, dc:type | schema:additionalType |
| Optional | Contributor to the resource’s creation | dcterms:contributor, dc:contributor | schema:contributor |
| Optional | Format of the resource | dcterms:format, dc:format| schema:encodingFormat |
| Optional | Information on the source (e.g. journal issue) | dcterms:relation, dc:relation | schema:mentions |
| Optional | Temporal coverage of the resource | dc:coverage, dcterms:coverage | schema:temporalCoverage |
| Optional | Spatial coverage of the resource | dcterms:spatial | schema:spatialCoverage |



*Priority*.  
The *mandatory* elements are necessary for the platform to process the metadata. The *recommended* elements increase both the findability of the contents and the quality of the automated processes run by the platform. The *optional* elements can provide additional information useful for the users.

*DublinCore elements*.  
The simple DC elements are introduced by the `dc` namespace, the qualified DC elements are introduced by the `dcterms` namespace. While it is still technically possible to use simple DC, it is preferable to use QDC, which allows for a more detailed description of the resource.   
In some cases, it is possible to use one or many DC elements to describe an aspect of the resource: the date of the resource can be described through `dcterms:date` or through the more accurate  `dcterms:created` and  `dcterms:available`.

*TRIPLE data model*.  
The elements of the TRIPLE data model in the schema.org ontology are reported only for information: these are handled only by the GoTriple platform, not by the content providers.   
Some of the DC and QDC elements are processed by the platform. This is especially the case for "URL of the landing page" and "URL of the resource", which are automatically determined from the content of `dcterms:identifier` or `dc:identifier`.
The TRIPLE data model also contains a few other elements for documents that are created through the analysis of the metadata files.

## Best practices for contents' visibility
### Metadata quality
While only three metadata elements are technically mandatory on GoTriple, richer metadata improve the processing by the information systems and therefore increases the visibility of the contents. Some of the metadata elements require however more accurate management in order to fully exploit the potentialities of the DublinCore standard. We list below a few hints able to improve the metadata quality in the context of GoTriple, but also in the context of other aggregators, like OpenAIRE, DOAJ, DOAB or BASE.

| Priority | Description | Hints and comments | 
| :---     |    :----:   | :---     | 
| Mandatory | Creator of the resource| Can contain one or many creators of the resource and can be individuals or organizations. On GoTriple, person names undergo a normalization process able to improve the filtering. |
| Mandatory | Identifier of the resource| Can contain one or many identifiers of different types. Identifiers are non semantic strings of characters uniquely identifying a resource. They should belong to a well-known identification system (e.g. ISBN, DOI, handle.net, etc.). <br/>In the digital context, the more important identifier is the Persistent Identifier (PID), which ensures the persistent identification of the resource throughout the various digital locations. Persistent identifiers include among others: DOI from Datacite or Crossref, handles from handle.net.<br/>Identifiers should be provided as HTTP links and can be specified through dedicated encoding schemes accepted by the DC standard (e.g. URI, DOI, ISBN). | 
| Mandatory | Title of the resource | Titles are used for automated enrichments on GoTriple. They shouldn't be or contain a file name. |
| Recommended | Abstract  | The `dcterms:description` can be more extended than the `dcterms:abstract`, or contain an abstract. On GoTriple, abstracts are used for the automated classification. |
| Recommended | Access rights to the resource | Can contain free text information about the possible access to the resource. As recommended also by OpenAIRE, it is possible to specify the access type in a normalized way through the [COAR access rights types](https://vocabularies.coar-repositories.org/access_rights/): embargoed access; metadata only access; open access; restricted access. Access information can be complemented with licensing information. |
| Recommended | Date of publication or creation  | Without more precise information, the `dcterms:date` or `dc:date` element will be interpreted on GoTriple as "resource's first release date". Although the `date` element is normalized on GoTriple, it is preferable to use standardized date formats, like for instance [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html). Date or period related not to the resource, but to its content, should be indicated in `dcterms:coverage`. |
| Recommended | Keywords  | Can contain one or many keywords describing the content of the resource. In DC, the keywords language can be specified using an `xml:lang` attribute. Best practice is to use the [ISO 639-3](https://iso639-3.sil.org/) three-letters code to identify the language |
| Recommended | Language of the resource | Describes the language in which the resource is expressed. Like for keywords, best practice is to use the [ISO 639-3](https://iso639-3.sil.org/) three-letters code. | 
| Recommended | License |  |
| Recommended | Publisher of the resource |  |
| Recommended | URL of the landing page |  |
| Recommended | URL of the resource |  |
| Recommended | URL of the source (e.g. URL of a publishing platform) | L |
| Optional | Type of the resource |  |
| Optional | Contributor to the resource’s creation |  |
| Optional | Format of the resource |  |
| Optional | Information on the source (e.g. journal issue) |  |
| Optional | Temporal coverage of the resource |  |
| Optional | Spatial coverage of the resource |  |

### FAIR principles
### Aggregators 

## Process
### Architecture
### Quality control
### Enrichment

## Support for the providers
### Dashboard

## Credits

## Annexe
### Glossary
**Aggregator**

**Core pipeline**

**Dataset**

**Document**

**Harvester**

**Provider**

**Publication**

### Terms of Agreement

### GoTriple list of content types
-   archival material
-   art exhibition
-   article
-   bibliography
-   blog post
-   book
-   bulletin
-   conference
-   course
-   dataset
-   digital library
-   image
-   learning object
-   manuscript
-   map
-   multimedia
-   periodical
-   preprint
-   report
-   review
-   score
-   seminar
- slideshow
-   software
-   survey data
-   text
-   thesis
-   web_page
-   other

