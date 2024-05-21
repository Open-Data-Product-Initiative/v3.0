---
title: Open Data Product Specification 3.0 | Enabling Data Economy 

language_tabs: # must be one of https://git.io/vQNgJ
- yaml

toc_footers:
  - License <a href='https://www.apache.org/licenses/LICENSE-2.0'>Apache 2.0</a>
  - <br/><a href='https://opendataproducts.org'>Specification home</a>

includes:
  - sla
  - qa
  - pricing
  - license
  - dataops
  - dataaccess
  - dataholder
  - extensions
  - helloworld
  - bareminimum
  - terms
  - contributors

search: true

code_clipboard: true

meta:
  - name: description
    content: The Open Data Product Specification is a vendor-neutral, open-source machine-readable data product metadata model. It defines the objects and attributes as well as the structure of digital data products. 
---

# OPEN DATA PRODUCT SPECIFICATION 3.0 

## Production version 

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “NOT RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as shown here.

**VERSION 3.0**


**Version source:**

* <a href="https://github.com/Open-Data-Product-Initiative/v3.0">https://github.com/Open-Data-Product-Initiative/v3.0</a>

**ODPS YAML Schema:**

* <a href="https://opendataproducts.org/v3.0rc/schema/odps.yaml">YAML Schema</a>

**Editors:**

* <a href="https://www.linkedin.com/in/jarkkomoilanen/">Jarkko Moilanen</a>
* <a href="https://www.linkedin.com/in/jussi-niilahti/">Jussi Niilahti</a>


**Participate:**

* [Raise an issue in Github](https://github.com/Open-Data-Product-Initiative/v3.0/issues)

## Introduction

The Open Data Product Specification is a vendor-neutral, open-source machine-readable data product metadata model. It defines the objects and attributes as well as the structure of digital data products. The work is based on existing standards (schema.org), best practices and emerging concepts like Data Mesh. The reasoning is that we reuse and proudly copy instead of reinventing the wheel. More detailed information of the origin can be found from the [Open Data Product Specification homepage](http://www.opendataproducts.org). 

Open Data Product Specification (ODPS) changes the data product metadata model towards a standalone model, which helps to decouple data product from the systems often directly associated with it. With help of the ODPS data product can be presented and described to the customer also as such without any need for marketplace or other systems. 

This version signifies a step towards embracing Everything as Code paradigm, but is still experimental. Both SLA and Data quality support now "as code" monitoring.   


Development of the standard is coordinated in Open Data Product Initiative (ODPI) which was established in July 2022 to make it possible for the specification to grow and become institutionlized. The ODPI was taken under the wings of open source chapter of Open Collective.

## Specification aims and aspects

**Specification aims:**

* enable interoperability between organizations, data platforms,  marketplaces, and tools. 
* reduce data product metadata conversions and errors between systems and organizations, 
* increase the speed of designing, testing, and implementing data products. 
* speed up tools development around data product design, development and management.
* enable creation of automated data product deployment with standard methods (DataOps)
* enable [Everything as Code](https://www.cloudbees.com/blog/what-is-everything-as-code-eac) approach for SLA and Data Quality monitoring

**Note!** In the "Open Data Product" focus is on the latter words and the prefix  'open' refers to the openness of the standard. Any kind of connotations to open data (a different thing) are not intentional, intended, or desirable.

The specification has been designed with four major aspects of the data product in mind: 1) technical (infrastructure & access), 2) business (pricing & plans), 3) legal (licensing & IPR), and 4) ethical (privacy & mydata). The four aspects are described in 7 elements, which contain attributes and other elements. 

![odps-model](images/ODPS-design.png)


If you see something missing, described inaccurately or plain wrong, or you want to comment the specification, [raise an issue in Github](https://github.com/Open-Data-Product-Initiative/v3.0/issues)

## Document structure

**LEFT COLUMN: Navigation**

The left column is navigation which enables fluent and easy movement around the specification. 

**MIDDLE COLUMN: Principles and components**

The middle column contains detailed information about the included components and related options. This is the theory part. 

Note! Mandatory elements and attributes are listed separately in the definition tables. This enables user to construct minimum viable specification more easily and fast. https://schema.org provided ready-made definitions are applied when ever possible instead of re-inventing the wheel. 

**RIGHT COLUMN: Examples**

The right column contains YAML formatted examples of how the specification is used. In the future other output formats are added on request basis. YAML can easily be converted to JSON if needed. 

> Example of YAML formatted snippet from the Open Data Product Specification:

```yml
monitoring:
  space: 
    https://monitoring.com
```


<aside class="notice">
The YAML examples are not based on any real data product, but exemplify the usage of Open Data Product Specification. 

</aside>


# Document level attributes

Here's the list of attributes which can occur at the document root level. In the following description, if a field is not explicitly **REQUIRED** or described with a MUST or SHALL, it can be considered OPTIONAL. Optional attributes are listed in own table and examples are given on the right column. 

## Mandatory attributes

> Example of document level attribute usage and structure:

```yml
schema: https://opendataproducts.org/v3.0rc/schema/odps.yaml
version: 3.0
product:
  details:
    en:
      name: Pets of the year
      productID: 123456are
      visibility: private
      status: draft
      type: dataset
    fi:
      name: Vuoden suosituimmat lemmikit
      productID: 123456are
      visibility: private
      status: draft
      type: dataset
```

| <div style="width:150px">Element name</div>   | Type  | Options  | Description  |
|---|---|---|---|
| **schema** | URL | Valid URL. See more from [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986). | **REQUIRED** Defines the URL of Schema. Used often for validation purposes. |
| **version** | string | This is the version of ODPS, for example dev or 2.2 | **REQUIRED** Defines the ODPS version. |
| **product** | element | root element | **REQUIRED** Root element to tie all together. |
| **details** | element | product business details | **REQUIRED** Binds together business details in different languages. |
| **en** | element | [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) defined 2-letter codes | **REQUIRED** - **NOTE! This is a dynamic element!** This element binds together other product attributes and expresses the langugage used. In the example this is "en", which indicates that product details are in English. If you would like to use French details, then name the element "fr". The naming of this element follows options (language codes) listed in [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) standard. <br/><br/> You can have product details in multiple languages simply by adding similar sets like the example - just change the binding element name to matching language code. <br/><br/> The pattern to implement multilanguage support for data products was adopted from de facto UI translation practices. The attributes inside this element are commonly rendered in the UI for the consumer and providing a simple way to implement that was the driving reasoning. See for example  [JSON - Multi Language](https://simplelocalize.io/docs/file-formats/multi-language-json/) |
| **name** | string | max length 256 chars | **REQUIRED** The name of the product. |
| **productID**  | string | max length 256 chars | **REQUIRED** Product identifier. |
| **visibility**  | one of | one of: private, invitation, organisation, dataspace, public | **REQUIRED** The publicity level eg who can see this product. Private - just the creator. Invitation - visible only to parties explicitly invited. Organisation - visible to all in your organisation. Dataspace - visible to all existent members of the data space. Public - visible to all publicly. |
| **status**  | one of | one of: announcement, draft, development, testing, acceptance, production, sunset, retired | **REQUIRED** The status of the product. Lifecycle model discussed in details in here (link). |
| **type** | one of |  Options: raw data, derived data, dataset, reports, analytic view, 3D visualisation, algorithm, decision support, automated decision-making, data-enhanced product, data-driven service, data-enabled performance, bi-directional. | **REQUIRED** The type of the product. Options are derived from examples and lists found from academic literature.  | 


## Optional attributes

RecommendedDataProducts **OBJECT** contains an array of data products which offers means to attach related data products to the data product at hand. The source of the recommended data product might be from the same marketplace/catalog or an external one. Recommended object offers method to extend the reach and promotion escpecially when data product is treated as an independent entity much like described in Data Mesh. Also when data product is published in a marketplace, the Recommended object offers means to promote other than just the data products from the given data marketplace. In short, tis object is mainly for discovery and reach purposes. 

RecommendedUseCases **OBJECT** is an array which contains offers method to attach usefull usecases to the data product. Usecases are informatiove for the the data customer and exemplify how the data product can create value. 

> Example of document level attribute usage and structure:

```yml
schema: https://opendataproducts.org/v3.0/schema/odps.yaml
version: 3.0
product:
  details: 
    en:
      name: Pets of the year
      productID: 123456are
      valueProposition: Design a customised petstore using a data product that describes
        pets with their habits, preferences and characteristics.
      description: This is an example of a Petstore product.
      productSeries: Lovely pets data products
      visibility: private
      status: draft
      productVersion: '0.1.0'
      versionNotes: New version with additional details such more accurate pet details
      issues: The current issues include incorrect information in the dog breeds. The
        resolution for these problems is planned for the next     update, scheduled
        to be released on July 15th, 2023.
      categories:
      - pets
      standards:
      - ISO 24631-6
      tags:
      - pet
      brandSlogan: Passion for the data monetization
      type: dataset
      contentSample: https://download.com/pets.json
      logoURL: https://data-product-business.github.io/open-data-product-spec/images/logo-dps-ebd5a97d.png
      OutputFileFormats:
      - JSON
      - XML
      - CSV
      - ZIP
      - PDF
      useCases:
      - useCase:
          useCaseTitle: Build attractive and lucrative petstore!
          useCaseDescription: Use case description how succesfull petstore chain was
            established in Abu Dhabi
          useCaseURL: https://marketplace.com/usecase1
      recommendedDataProducts:
      - https://marketplace.com/dataproduct.json
      - https://marketplace.com/dataproduct-another.json

```

| <div style="width:150px">Element name</div>   | Type  | Options  | Description  |
|---|---|---|---|
| **created**  | date | Use [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) | When product was created. | 
| **updated**  | date | Use [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) | When product was last updated. |
| **valueProposition** | string  | text content, max length 512 chars  | This is the product's value proposition. Often one or two sentences and crystallizes the value for the customer. |
| **description** | string | - | The description of the product. Text only. |
| **productSeries** | string | - | A group of products in the product mix which are associated with each other and they can be obtained for the same type of customers or they are marketable for the same type of market place. |
| **categories** | array | - | Comma separated array of categories. |
| **standards** | array | - | Comma separated array of standards related e.g. to data content or quality, such as ISO 8000 or ISO 19131. |
| **tags** | array | - | Comma separates array of tags. |
| **productVersion** | string | The versioning according to [SemVer](https://semver.org/) | The version of the data product. Applies for ODPS metadata as well. |
| **versionNotes** | string | - | Additional information about the version. |
| **issues** | string | - |  There may be errors in the data product that require corrections. These issues will be briefly described to users, along with information about when the fixes will be implemented.|
| **contentSample** | URL | Valid URL. See more from [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986). | Sample content of the data product, for example JSON/XML output. This sample should match the actual data product output and give the data consumer an idea what to expect. Obviously if the data product is pure service for example dashboard or algorithm, then consider providing preview version or alike |
| **logoURL** | URL | Valid URL | Valid URL of the logo. See more from [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986). |
| **outputFileFormats** | string | - | Output file formats for data product |
| **brandSlogan** | string | - | Brand related slogan like Nike has *just do it*. |
| **useCases** | element | array | Contains list of related use cases with description information and link to details. **NOTE!** These examples are expected to use same language as defined previously in the data product details content binding element. |
| **useCaseTitle**| string | string | Title of the usecase. |
| **useCaseDescription** | string | string | Brief description of the usecase. |
| **useCaseURL**| URL | Valid URL, [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986) | Valid URL of the more detailed usecase description. |
| **recommendedDataProducts** | array | Array of valid URLs ([RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986)) | Data products to recommend use next to this data product or even as replacement (for comparison). The URL provided MUST reference a description of a data product following this same standard |

If you see something missing, described inaccurately or plain wrong, or you want to comment the specification, [raise an issue in Github](https://github.com/Open-Data-Product-Initiative/v3.0/issues)
