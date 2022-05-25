
***WORK IN PROGRESS***
-----

# GoTriple Content Providers Handbook 
<br>[**1. Purpose of this document**](#purpose-of-this-document)
<br>[**2. GoTriple policies**](#gotriple-policies)
<br>[2.1 Scope](#scope)
<br>[2.2 Content types](#content-types)
<br>[**3. GoTriple requirements**](#gotriple-requirements)
<br>[3.1 Technical set-up](#technical-set-up)
<br>[3.2 GoTriple data model](#gotriple-data-model)
<br>[**4. Best practices**](#best-practices-for-contents-visibility)
<br>[4.1 Metadata quality](#metadata-quality)
<br>[4.2 FAIR principles](#fair-principles)
<br>[4.3 Aggregators](#aggregators)
<br>[**5. Process**](#process)

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

The list of content types available on GoTriple is based on a subset of the [COAR list of types](https://vocabularies.coar-repositories.org/resource_types/)  (see [Annexe](#gotriple-list-of-content-types)).   
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
| Recommended | Access rights to the resource | dcterms:accessRights, ??dcterms:conditions??, ??dc:conditions?? |schema:conditionsOfAccess |
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
| Mandatory | Creator of the resource| Can contain one or many creators of the resource and can be individuals or organizations ??from DCMI??. On GoTriple, person names undergo a normalization process able to improve the filtering. |
| Mandatory | Identifier of the resource| Can contain one or many identifiers of different types. Identifiers are non semantic strings of characters uniquely identifying a resource. They should belong to a well-known identification system (e.g. ISBN, DOI, handle.net, etc.). <br/>In the digital context, the more important identifier is the Persistent Identifier (PID), which ensures the persistent identification of the resource throughout the various digital locations. Persistent identifiers include among others: DOI from Datacite or Crossref, handles from handle.net.<br/>Identifiers should be provided as HTTP links and can be specified through dedicated encoding schemes accepted by the DC standard (e.g. URI, ??DOI, ISBN)??. | 
| Mandatory | Title of the resource | Titles are used for automated enrichments on GoTriple. They shouldn't be or contain a file name. |
| Recommended | Abstract  | The `dcterms:description` can be more extended than the `dcterms:abstract`, or contain an abstract. On GoTriple, abstracts are used for the automated classification. |
| Recommended | Access rights to the resource | Can contain free text information specifically about the access to the resource. As recommended also by OpenAIRE, it is possible to specify the access type in a normalized way through the [COAR access rights types](https://vocabularies.coar-repositories.org/access_rights/): embargoed access; metadata only access; open access; restricted access. Access information can be complemented with licensing information. |
| Recommended | Date of publication or creation  | Without more precise information, the `dcterms:date` or `dc:date` element will be interpreted on GoTriple as "resource's first release date". Although the `date` element is normalized on GoTriple, it is preferable to use standardized date formats, like for instance [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html). Date or period related not to the resource, but to its content, should be indicated in `dcterms:coverage`. |
| Recommended | Keywords  | Can contain one or many keywords describing the content of the resource. In DC, the keywords language can be specified using an `xml:lang` attribute. Best practice is to use the [ISO 639-3](https://iso639-3.sil.org/) three-letters code to identify the language |
| Recommended | Language of the resource | Describes the language in which the resource is expressed. Like for keywords, best practice is to use the [ISO 639-3](https://iso639-3.sil.org/) three-letters code. | 
| Recommended | License | A legal document indicating how the resource can be accessed and used. In QDC, there is a specific element for the licensing information: `dcterms:license`. This element can also contain information about copyright and intellectual property rights.<br/>While a license can be a free text, it is preferable to use standardized licenses: they are easier to understand for humans and can facilitate machine-readibility. In the context of open science, especially, it is recommended to use well-spread open licenses, for example [Creative Commons (CC) licenses](https://creativecommons.org/about/cclicenses/). The CC licenses allow to indicate an URL and to indicate the license type in a simple way.|
| Recommended | Publisher of the resource | An entity responsible for making the resource available. Can be a person, an organization, like a publishing company or a service, like a data archive. The `publisher` element describes the resource and its production, not the creator and its affiliations. |
| Recommended | URL of the landing page | The URL of the landing page can be indicated as a specific `dcterms:identifier` or `dc:identifier` element using the URI scheme.  |
| Recommended | URL of the resource | Like the URL of the landing page, the URL of the resource itself can be indicated as a specific `dcterms:identifier` or `dc:identifier` element using the URI encoding scheme. In GoTriple, the URLs listed in the ìdentifier` elements containing a .pdf extension are used to create the direct link to the full text.  |
| Recommended | URL of the source | A related resource from which the described resource is derived. In GoTriple, `dcterms:source`and `dc:source` elements ??are used to refer to the publishing platform or data repository.?? |
| Optional | Type of the resource | The type of the resources should refer to a well-spread taxonomy, like the aforementioned [COAR list of types](https://vocabularies.coar-repositories.org/resource_types/), or the subset of COAR types listed in [Annexe](#gotriple-list-of-content-types). |
| Optional | Contributor to the resource’s creation | An entity responsible for making contributions to the resource. Other than the entities that have contributed to the creation of the resource (e.g. a data scientist for a dataset, an editor for a publication), the `contributor` element can be used to list the organizations that have made the creation possible. |
| Optional | Format of the resource | The file format, physical medium, or dimensions of the resource. Recommended practice is to use a controlled vocabulary where available. For example, for file formats one could use the list of [MIME Internet media types](https://www.iana.org/assignments/media-types/media-types.xhtml)|
| Optional | Information on the source (e.g. journal issue) | This element is used for instance to indicate the relation of an article with a specific journal issue. |
| Optional | Temporal coverage of the resource | In the DublinCore standard, `dc:coverage` and `dcterms:coverage` contain information about temporal and spatial coverage. In GoTriple, these elements are used only for the temporal coverage. Spatial coverage should be indicated in `dcterms:spatial` . |
| Optional | Spatial coverage of the resource | Contains free or standardized text about the spatial area considered by the resource. The element is only available in QDC: `dcterms:spatial` .  |

### FAIR principles
The FAIR principles emerged in 2016 from an interdisplinary group of research data experts. The acronym FAIR refers to four guiding principles for digital data management: making the data Findable, Accessible, Interoperable, and Reusable. The FAIR principles address the need for a common understanding of data management good practices able to facilitate data sharing and reuse. Although the principles mainly consider technical aspects, they allow, as principles, to adapt the concrete implementations to specific contexts. In particular, they can apply to any research digital object: datasets, publications, software, etc.<br/>

The four ground principles are further described in a set of fifteen principles. [GOFAIR](https://www.go-fair.org), the organisation supporting the FAIR principles adoption, gives detailed information about [the fifteen FAIR principles](https://www.go-fair.org/fair-principles/). The OPERAS Special Interest Group on "Common standards and FAIR principles" also provided an overview in its [2021 White paper](https://www.operas-eu.org/special-interest-group-living-book/operas-common-standards-white-paper-june-2021/#Common-Standards-2021-FAIR).<br/>

The FAIR principles are a useful tool to manage digital data in a way that facilitates both human and machines operations. They have been used to built the TRIPLE data model and are now at the core of all major aggregators practices.  
The **Findability** principle relies mainly on the use of persistent identifiers and rich descriptive metadata. The metadata should give information about the resource, like: creator, title, persistent identifier, publisher, publication date, abstract and keywords. A counterexample is a corpus stored on a USB device with descriptive information only in the file name.  
The **Accessibility** principle relies on the use of open, free and documented protocols, such as HTTP, OAI-PMH, FTP, even if they are combined with authentication processes. Accessibility is further improved if metadata gives information about the conditions of access. A counterexample is the data exchanged through emails on individual request.  
The **Interoperability** principle relies on the use of standard representation of the data, like the DublinCore schema aforementioned. Interoperability can also be reached thanks to documented controlled vocabularies shared within a broad community. A counterexample is a dataset described according to an individual and not documented vocabulary.  
The **Reusability** principle relies on clear licensing information, as liberal as possible, preferably standard and recorded in the metadata. It should be completed with clear provenance information, which allows to better assess the reusability possibilities. A counterexample, without mentioning the lack of any license, is a license containing unclear conditions of use in a separate PDF file.<br/>

The TRIPLE data model follows the main aspects of the FAIR principles and this handbook will help you to ensure that your content is Findable, Accessible, Interoperable, and Reusable.






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

