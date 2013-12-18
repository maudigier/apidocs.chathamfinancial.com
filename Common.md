!Common API Components
=======================

## Required Components
The following components are required to be on every request made to the API.

### Authorization
-----

#### **[OAuth 2.0](http://tools.ietf.org/html/rfc6749) Access Token**

Each request is required to have an access token in the `Authorization` header of the request. The access token is provided by Chatham.

The format is:

```text
Authorization: Bearer <AccessToken>
```

Replace `<Access Token>` with the Chatham provided access token. See [RFC 6750](http://tools.ietf.org/html/rfc6750) for more information.

*Example:*

```text
Authorization: Bearer 6879dcb0789ef62a0789d509ff624a98c9809b66
```
#### **Related Status Codes**

|  Status Code  | Description                                    |
| :-----------: | ---------------------------------------------- |
| `401`         | You are not authorized to access the resource. |

-----
## Optional Components
The following components are optional and not required to be on each request. Each component may not be valid on every request, see notes for that component.

### Content Type
-----
You can specify the content type of the response by setting the `Accept` header in the request. All requests support setting the `Accept` header.

*Example:*

```text
Accept: application/json
```

Supported Content Types:
* `application/json`

The default content type is `application/json` if the `Accept` header is missing from the request. See [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) for more information.

#### **Related Status Codes**

|  Status Code  | Description                        |
| :-----------: | ---------------------------------- |
| `415`         | The content type is not supported. |

-----

### Compression

-----
All requests support compressed responses. Include `Accept-Encoding` header with a supported compression in your request to get a compressed response.

*Example:*

```text
Accept-Encoding: gzip,deflate
```

Supported Compression:

* `gzip`
* `defalte`

See [RFC 2616 Section 14.3](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.3) for more information.

-----

###  [Partial Responses](https://github.com/AnthonyCarl/ServiceStack.PartialResponse)

-----
Partial Responses are supported on most requests. Partal Responses will limit the information in the response. 

* Field selectors are provided either in the header or query string. 
* If a request has field selectors in the query string and header, they will be combined (duplicates ignored).
* Field selectors that reference non-existent fields are ignored.
* If a field selector is for a nested object, all fields of the nested object will be returned unless a specific field on the nested object is selected.
* If a field selector is for a field on a list item, that field will be returned for all items in the list.

| Method         | Example                                                                                                           |
|:--------------:|:------------------------------------------------------------------------------------------------------------------|
| `Query String` | `https://api.chathamfinancial.com/reports/transactions?fields=items(Id,EffectiveDate,Notional,NotionalCurrency)`* |
| `Header`       | `x-fields: items(Id,EffectiveDate,Notional,NotionalCurrency)`                                                     |
*Query string should be [URL encoded](http://meyerweb.com/eric/tools/dencoder/) i.e. `https://api.chathamfinancial.com/reports/transactions?fields=items(Id%2CEffectiveDate%2CNotional%2CNotionalCurrency)`. Shown unencoded for clarity.

#### **Field Selector Syntax**
| Character | Meaning                            |
|:---------:|:-----------------------------------|
| `,`       | Separates multiple field selectors |
| `/`       | Field sub selector                 |
| `(`       | Begin subselection expression      |
| `)`       | End subselection expression        |

**NOTE**: Field Selectors may be nested.

#### **Partial Response Supported Content Types**
* `application/json`

If an unsupported content type is requested for a partial response, the field selectors will be ignored.

#### **Related Status Codes**

|  Status Code  | Description                                                                             |
| :-----------: | --------------------------------------------------------------------------------------- |
| `414`         | URI is too long. Consider putting some or all field selectors in the `x-fields` header. |

-----

### Pagination
----
Responses that are collections are paged.

| Query String Parameter    | Default | Min Value | Max Value         | Description                                       |
| ------------------------- | ------- | --------- | ----------------- | ------------------------------------------------- |
| offset                    | `0`     | `0`       | `total items - 1` | Index of the first record to return (zero based). |
| limit                     | `100`   | `1`       | `500`             | Specifies the maximum number of items to return.  | 

* If the `previous` link is not present in the `Link` header, you are at the beginning of the collection.
* If the `next` link is not present in the `Link` header, you are at the end of the collection.

#### **Typical Paged Response**

**[Link Header](http://tools.ietf.org/html/rfc5988)**

```text
Link: <?limit=2&offset=2>;
      rel="previous",
      <?limit=2&offset=4>;
      rel="self",
      <?limit=2&offset=6>;
      rel="next",
      <?limit=2&offset=0>;
      rel="first",
      <?limit=2&offset=8>;
      rel="last"
```

**Message Body**

```json
{
    "Paging": {
        "Limit": 2,
        "Offset": 4,
        "TotalItems": 10
    },
    "Items": [
        { ...item1... },
        { ...item2... }
	]	
}
```

----
