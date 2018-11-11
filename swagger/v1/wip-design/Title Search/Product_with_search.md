Product API
===========
HUK API To Access HUK products.

Our new Bibliographic API will allow you to access our Product data. 
Currently this is a Read-Only API (GET methods), which includes Images
and catregorization.

## Endpoints
Currently we have two endpoints.

### Test
hachetteuk-test.apigee.net 

### Production
hachetteuk-prod.apigee.net


**Version:** 1.0.6

### Security
---
**APIKeyHeader**  

|apiKey|*API Key*|
|---|---|
|In|header|
|Name|x-apikey|

### /products
---
##### ***GET***
**Summary:** Gets a list of Products

**Description:** Gets a list of `product` objects - normally books.

Optional query param of **limit** determines
size of returned array


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| filterByTimestamp | query | Get products updated since this date & time. Please note we require you to `convert to UK GMT`. Format is:   YYYY-MM-DDTHH:MM:SS   YYYY = Year  MM = Month  DD = Day  T = Time  HH = Hour - 24 hour  MM = Minute  SS = Seconds  Example format - 2018-07-04T09:00:00  | No | string |
| filterByImprints | query | Filters products with one of these Imprints. | No | [ string ] |
| filterByDivisions | query | Filters products with one of these Divisions. | No | [ string ] |
| filterByIsActive | query | Filters product which are Active (or not). | No | boolean |
| editionId | query | Get a product with its editionId. | No | number |
| limit | query | Size of collection to be returned. | No | number (integer) |
| page | query | Page number you wish returned. | No | number |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | object |
| 204 | No content found. |  |
| 401 |  |  |

### /products/{isbn13}
---
##### ***GET***
**Summary:** Get a Product using its ISBN13

**Description:** Gets `product` object (normally a book).


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| isbn13 | path | ISBN13 to fetch | Yes | string |
| limit | query | Size of collection to be returned. | No | double |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response containing a Hachette product | [Product](#product) |
| 204 | No content found. |  |
| 401 |  |  |

### /products/search/{title}
---
##### ***GET***
**Summary:** Search for a Product using its Title.

**Description:** Gets `product` search objects.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| title | path | Title to search with. | Yes | string |
| filterByImprints | query | Filters products with one of these Imprints. | No | [ string ] |
| filterByDivisions | query | Filters products with one of these Divisions. | No | [ string ] |
| limit | query | Size of collection to be returned. | No | number (integer) |
| page | query | Page number you wish returned. | No | number |
| fuzzy | query | Use Fuzzy Search for Title | No | boolean |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response containing a Hachette product | [SearchProduct](#searchproduct) |
| 204 | No content found. |  |
| 400 | Issue with parameters passed into API. |  |
| 401 |  |  |

### /products/count
---
##### ***GET***
**Summary:** Gets a count of Product records.

**Description:** Gets a count of product records. Useful before Paginating and iterating through a collection.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| filterByTimestamp | query | Get products updated since this date & time. Please note we require you to `convert to UK GMT`. Format is:   YYYY-MM-DDTHH:MM:SS   YYYY = Year  MM = Month  DD = Day  T = Time  HH = Hour - 24 hour  MM = Minute  SS = Seconds  Example format - 2018-07-04T09:00:00  | No | string |
| filterByImprints | query | Filters products with one of these Imprints. | No | [ string ] |
| filterByDivisions | query | Filters products with one of these Divisions. | No | [ string ] |
| filterByIsActive | query | Filters product which are Active (or not). | No | boolean |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | object |
| 401 |  |  |

### Models
---

### Product  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| editionID | number | unique ID for this Edition. | No |
| coverTitle | string | Title that appears on the cover of this Edition. | No |
| isbn13 | string | ISBN13 which resides within the barcode. | No |
| isActive | boolean | Is the record active. | No |
| subTitle | string | If the product has a sub title, it will appear here. | No |
| coverAuthors | string | Author names who will appear on the product. | No |
| workReference | string | Reference related to this work. | No |
| binding | string | Example Paperback or Hardback. | No |
| division | string | Publishers name. | No |
| format | object | Format of the product. Example CD, MP3, Kindle etc | No |
| sortTitle | string | Title you can use in any sorting algorthims. | No |
| workID | string | Work ID links all the different versions if the product together. The number will be same for various products and these are linked as a 'Work'. | No |
| imprint | string | Imprint name. | No |
| pubDate | string | published date (or if in the future, to be published date) | No |
| productType | string | Type of Product. Example Book, App, Ebook. | No |
| seriesNumber | number | If a product is part of a Series, this represents N in Series. | No |
| seriesTitle | string | If a product is part of a Series, this represents the Series Title. | No |
| issuedNumber | number | If the product has been reissued, this number represents how many times. | No |
| minimumAge | number | Minimum age in months a product is aimed at. | No |
| maximumAge | number | Maximum age in months a product is aimed at. | No |
| description | string | Long Description of a product. | No |
| keynote | string | Short Description of a product. | No |
| status | string | Current status of the product (Confirmed, Abandoned etc). | No |
| copyRightYear | number | Copyright year. | No |
| pubPrice | number | published price of the product. | No |
| pageCount | number | Page count for the product. | No |
| keywords | [ string ] |  | No |
| editionTypes | [ number ] | These are the ONIX Edition Type codes | No |
| relatedProducts | [ string ] | Array of EANs that are related to this product. | No |
| timeStamp | string | Timestamp when record was updated Hachettes end. | No |
| people | object | Contributors of a Product is where you can find Authors etc | No |
| categories | object | Category of book | No |
| availability | object | Products availability. | No |
| reviews | object | Reviews of a Product. | No |
| images | object | Different Images for a Product. | No |
| awards | object | If a product is shortlisted, won, longlisted etc for an Award, it will be held here. | No |
| link | [Link](#link) |  | No |

### Person  

Person who contribute towards a Product.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | number |  | No |
| firstName | string | First Name of the Person. | No |
| lastName | string | Last Name of the Person. | No |
| role | string | The role the Person has made to the book. | No |
| code | string | Role ONIX Code. | No |
| link | [Link](#link) |  | No |

### CategoryTypes  

Category Types

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| CategoryTypes | string | Category Types |  |

### BISAC  

Book Industry Communication (BIC) Codes

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| categorytype | string |  | No |
| code | string |  | No |
| description | string |  | No |
| version | string |  | No |
| mainCode | boolean | Main code for this version. If true, if you have multiple versions, use the code mainCode=true as the main category. | No |

### BIC  

Book Industry Study Group (BISAC) Code

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| categorytype | string |  | No |
| code | string |  | No |
| description | string |  | No |
| version | string |  | No |
| mainCode | boolean | Main code for this version. If true, if you have multiple versions, use the code mainCode=true as the main category. | No |

### Thema  

Thema Subject Category (Thema is latin for 'Subject')

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| categorytype | string |  | No |
| code | string |  | No |
| description | string |  | No |
| version | string |  | No |

### Format  

Format codes,

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| categorytype | string |  | No |
| code | string |  | No |
| description | string |  | No |
| version | string |  | No |

### Relations  

Relationships exposed for Links

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Relations | string | Relationships exposed for Links |  |

### Link  

Links/Relationships to other Resources.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string |  | No |
| method | string |  | No |
| rel | string |  | No |

### Availability  

Product availability.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string | Availability code. | No |
| description | string | Availability description. | No |

### Review  

Reviews of a Product.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | number | unique ID for the review. | No |
| editionId | number | Edition this review relates to. | No |
| reviewText | string | The actual review marketing text. | No |
| reviewer | string | The person/company who conducted the review. | No |
| source | string | Website/Newspaper/Blog etc the review appeared in. | No |

### Image  

Images associated with the Product.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| url | string | URL to download the image | No |
| type | string | Image Type. | No |

### Award  

Awards one for a Product or awards shortlisted for.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | number | Id of the Award | No |
| editionId | string | Edition Id the Award is linked to. | No |
| title | string | Title/Description of the Award. | No |
| announcedDate | string | Date & time the Award was announced publicly. | No |
| stage | string | Stage at which the product got in the Award system. | No |

### recordCount  

count record

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| count | number | Count of records. | No |

### SearchProduct  

Record receives when doing a search

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| isbn13 | string | ISBN13 which resides within the barcode. | No |
| coverTitle | string | Title that appears on the cover of this Edition. | No |
| subTitle | string | If the product has a sub title, it will appear here. | No |
| division | string | Publishers name. | No |
| imprint | string | Imprint name. | No |