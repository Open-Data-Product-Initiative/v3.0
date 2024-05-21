# Data Holder

DataHolder **Object** describes the **Organization legally allowed to create, develop and publish data products.** 

*Data holder* means "a legal person, public body, international organisation, or a natural person who is not a data subject with respect to the specific data in question, which, in accordance with applicable Union or national law, has the right to grant access to or to share certain personal data or non-personal data." (Data Governance Act)

The *data holder* might not be the original IPR owner of the data used, but has rights operate with it. The contract or other agreement between Provider and possible data owner is not part of the standard as metadata or licence wise.

If you see something missing, described inaccurately or plain wrong, or you want to comment the specification, [raise an issue in Github](https://github.com/Open-Data-Product-Initiative/v3.0/issues)


## Optional attributes and elements

> Example of Holder component with some of the voluntary attributes:

```yml

dataHolder:
  en:
    legalName: MindMote Oy
    businessId: 12243434-12
    email: contact@mindmote.fi
    taxID: "12243434-12"
    vatID: "12243434-12"
    logoURL: "https://mindmote.fi/logo.png"
    description: "Digital Economy services and tools"
    URL: "https://mindmote.fi"
    telephone: "+35845 0232 2323"
    streetAddress: "Koulukatu 1"
    postalCode: "33100"
    addressRegion: "Pirkanmaa"
    addressLocality: "Tampere"
    addressCountry: "Finland"
    aggregateRating: ""
    ratingCount: "1245"
    slogan: ""
    parentOrganization: ""
      
```

| <div style="width:150px">Element name</div>   | Type  | Options  | Description  |
|---|---|---|---|
| **dataHolder** | element | - | Binds the provider related business elements and attributes together |
| **en** | attribute | [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) defined 2-letter codes | This element binds together other product attributes and expresses the langugage used. In the example this is "en", which indicates that product details are in English. If you would like to use French details, then name the element "fr". The naming of this element follows options (language codes) listed in [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) standard. <br/><br/> You can have product details in multiple languages simply by adding similar sets like the example - just change the binding element name to matching language code. <br/><br/> The pattern to implement multilanguage support for data products was adopted from de facto UI translation practices. The attributes inside this element are commonly rendered in the UI for the consumer and providing a simple way to implement that was the driving reasoning. See for example  [JSON - Multi Language](https://simplelocalize.io/docs/file-formats/multi-language-json/) |
| **legalName** | string  | text content, max length 256 chars  | **REQUIRED** The official name of the organization, e.g. the registered company name.  | 
|  **businessID**| string  | As defined in [RFC 5322](https://datatracker.ietf.org/doc/html/rfc5322)  |  The business identifier code of the company. Often this is given to the company by authorized public sector organization managing register of businesses.  |
| **contactName** | string | - | Contact person name |
| **email** | string | - | Email to be used in contacting the organization. |
| **taxID** | string  | - | The Tax / Fiscal ID of the organization or person, e.g. the TIN in the US or the CIF/NIF in Spain. |
| **vatID** | string | - | The Value-added Tax ID of the organization or person. |
| **businessDomain** | string | - |  In a data mesh architecture, data (or data product) ownership and management are distributed across self-contained business domains. |
| **logoURL** | URL | Valid URL. See more from [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986). | The URL pointing to organisation logo. |
| **description** | string | Max length 512 chars | The introduction to the organization. Often contains information of what the organisation does and focuses on. |
| **URL** | URL | Valid URL. See more from [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986). | The URL of the organization's website.   |
| **telephone** | string | Valid telephone number | The telephone number. Use [E.164](https://www.itu.int/rec/T-REC-E.164-201011-I/en) standard.  |
| **streetAddress** | string | - | The street address. For example, 1600 Amphitheatre Pkwy.  |
| **postalCode** | string | - | The postal code. For example, 94043.  |
| **addressRegion** | string | - | The region in which the locality is, and which is in the country. For example, California or another appropriate first-level Administrative division |
| **addressLocality** | string | -  | The locality in which the street address is, and which is in the region. For example, Mountain View.  |
| **addressCountry** | string | two-letter ISO 3166-1 alpha-2 country code | The country.  |
| **aggregateRating** | string | - | The average rating based on multiple ratings or reviews. |
| **ratingCount** | integer | - | The amount of ratigns and reviews used in calculating the aggregateRating. |
| **slogan** | string | Max length 256 chars | The slogan of the organization. This is often related to showing the brand |
| **parentOrganization** | string | - | The larger organization that this organization is a subOrganization of, if any. |



If you see something missing, described inaccurately or plain wrong, or you want to comment the specification, [raise an issue in Github](https://github.com/Open-Data-Product-Initiative/v3.0/issues)
