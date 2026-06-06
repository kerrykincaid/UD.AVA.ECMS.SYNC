# Endpoints

<span style="color: rgb(224, 82, 0);">ListTransactionsByCompany  
## Retrieve all transactions

`GET /api/v2/companies/{companyCode}/transactions`

**API:** AvaTax API
**Tag:** Transactions
**Operation ID:** ListTransactionsByCompany
**API Version:** v2
**Base URL:** https://sandbox-rest.avatax.com/

Source: https://developer.avalara.com/products/avatax/api/methods/Transactions/ListTransactionsByCompany/

## Description

List all transactions attached to this company.
            
This endpoint is limited to returning 1,000 transactions at a time maximum.
            
When listing transactions, you must specify a `date` range filter.  If you do not specify a `$filter` that includes a `date` field
criteria, the query will default to looking at only those transactions with `date` in the past 30 days.
            
A transaction represents a unique potentially taxable action that your company has recorded, and transactions include actions like
sales, purchases, inventory transfer, and returns (also called refunds).
            
Search for specific objects using the criteria in the `$filter` parameter; full documentation is available on [Filtering in REST](http://developer.avalara.com/avatax/filtering-in-rest/) .
Paginate your results using the `$top`, `$skip`, and `$orderby` parameters.
            
You may specify one or more of the following values in the `$include` parameter to fetch additional nested data, using commas to separate multiple values:
            
* Lines
* Details (implies lines)
* AccountPayableSalesTaxDetails (implies lines - only for Account Payable transaction)
* Summary (implies details)
* Addresses
* SummaryOnly (omit lines and details - reduces API response size)
* LinesOnly (omit details - reduces API response size)
            
NOTE: If your companyCode or transactionCode contains any of these characters /, +, ? or a space please use the following encoding before making a request:
* Replace '/' with '\_-ava2f-\_'  For example: document/Code becomes document_-ava2f-_Code
* Replace '+' with '\_-ava2b-\_'  For example: document+Code becomes document_-ava2b-_Code
* Replace '?' with '\_-ava3f-\_'  For example: document?Code becomes document_-ava3f-_Code
* Replace '%' with '\_-ava25-\_'  For example: document%Code becomes document_-ava25-_Code
* Replace '#' with '\_-ava23-\_'  For example: document#Code becomes document_-ava23-_Code
* Replace ' ' with '%20'  For example: document Code becomes document%20Code

### Security Policies

* This API requires one of the following user roles: AccountAdmin, AccountOperator, AccountUser, AvaTaxOnlyAccountAdmin, AvaTaxOnlyAccountUser, AvaTaxOnlyCompanyAdmin, AvaTaxOnlyCompanyUser, BatchServiceAdmin, CompanyAdmin, CompanyUser, CSPAdmin, CSPTester, ProStoresOperator, ReturnsOnlyAccountAdmin, ReturnsOnlyAccountUser, ReturnsOnlyCompanyAdmin, ReturnsOnlyCompanyUser, SiteAdmin, SSTAdmin, SystemAdmin, TechnicalSupportAdmin, TechnicalSupportUser.
* This API depends on the following active services:*Required* (all):  AvaTaxPro, BasicReturns.

## Parameters

| Name | Type | In | Required | Description |
|---|---|---|---|---|
| `companyCode` | string | path | Yes | The company code of the company that recorded this transaction |
| `dataSourceId` | integer | query | No | Optionally filter transactions to those from a specific data source. |
| `$include` | string | query | No | Specifies objects to include in this fetch call |
| `$filter` | string | query | No | A filter statement to identify specific records to retrieve.  For more information on filtering, see [Filtering in REST](http://developer.avalara.com/avatax/filtering-in-rest/).*Not filterable:* exchangeRateCurrencyCode, totalDiscount, lines, addresses, locationTypes, summary, taxDetailsByTaxType, parameters, userDefinedFields, messages, invoiceMessages, isFakeTransaction, deliveryTerms, apStatusCode, apStatus, vendorName, varianceAmount |
| `$top` | integer | query | No | If nonzero, return no more than this number of results.  Used with `$skip` to provide pagination for large datasets.  Unless otherwise specified, the maximum number of records that can be returned from an API call is 1,000 records. |
| `$skip` | integer | query | No | If nonzero, skip this number of results before returning data.  Used with `$top` to provide pagination for large datasets. |
| `$orderBy` | string | query | No | A comma separated list of sort statements in the format `(fieldname) [ASC|DESC]`, for example `id ASC`. |
| `X-Avalara-Client` | string | header | No | Identifies the software you are using to call this API.  For more information on the client header, see [Client Headers](https://developer.avalara.com/avatax/client-headers/) . |

## Responses

| Status | Description |
|---|---|
| 200 | Success |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |

<span style="color: rgb(224, 82, 0);">GetTransactionById</span>  
## Retrieve a single transaction by ID

`GET /api/v2/transactions/{id}`

**API:** AvaTax API
**Tag:** Transactions
**Operation ID:** GetTransactionById
**API Version:** v2
**Base URL:** https://sandbox-rest.avatax.com/

Source: https://developer.avalara.com/products/avatax/api/methods/Transactions/GetTransactionById/

## Description

Get the unique transaction identified by this URL.
            
This endpoint retrieves the exact transaction identified by this ID number, as long as it is the most version of the transaction.
            
A transaction represents a unique potentially taxable action that your company has recorded, and transactions include actions like
sales, purchases, inventory transfer, and returns (also called refunds).
            
You may specify one or more of the following values in the `$include` parameter to fetch additional nested data, using commas to separate multiple values:
            
* Lines
* Details (implies lines)
* AccountPayableSalesTaxDetails (implies lines - only for Account Payable transaction)
* Summary (implies details)
* Addresses
* SummaryOnly (omit lines and details - reduces API response size)
* LinesOnly (omit details - reduces API response size)
* TaxDetailsByTaxType - Includes the aggregated tax, exempt tax, taxable and non-taxable for each tax type returned in the transaction summary.

### Security Policies

* This API requires one of the following user roles: AccountAdmin, AccountOperator, AccountUser, AvaTaxOnlyAccountAdmin, AvaTaxOnlyAccountUser, AvaTaxOnlyCompanyAdmin, AvaTaxOnlyCompanyUser, BatchServiceAdmin, CompanyAdmin, CompanyUser, CSPAdmin, CSPTester, ProStoresOperator, ReturnsOnlyAccountAdmin, ReturnsOnlyAccountUser, ReturnsOnlyCompanyAdmin, ReturnsOnlyCompanyUser, SiteAdmin, SSTAdmin, SystemAdmin, TechnicalSupportAdmin, TechnicalSupportUser.
* This API depends on the following active services:*Required* (all):  AvaTaxPro, BasicReturns.

## Parameters

| Name | Type | In | Required | Description |
|---|---|---|---|---|
| `id` | integer | path | Yes | The unique ID number of the transaction to retrieve |
| `$include` | string | query | No | Specifies objects to include in this fetch call |
| `X-Avalara-Client` | string | header | No | Identifies the software you are using to call this API.  For more information on the client header, see [Client Headers](https://developer.avalara.com/avatax/client-headers/) . |

## Responses

| Status | Description |
|---|---|
| 200 | Success |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |

<span style="color: rgb(224, 82, 0);">GetTransactionByCodeAndType  
## Retrieve a single transaction by ID

`GET /api/v2/transactions/{id}`

**API:** AvaTax API
**Tag:** Transactions
**Operation ID:** GetTransactionById
**API Version:** v2
**Base URL:** https://sandbox-rest.avatax.com/

Source: https://developer.avalara.com/products/avatax/api/methods/Transactions/GetTransactionById/

## Description

Get the unique transaction identified by this URL.
            
This endpoint retrieves the exact transaction identified by this ID number, as long as it is the most version of the transaction.
            
A transaction represents a unique potentially taxable action that your company has recorded, and transactions include actions like
sales, purchases, inventory transfer, and returns (also called refunds).
            
You may specify one or more of the following values in the `$include` parameter to fetch additional nested data, using commas to separate multiple values:
            
* Lines
* Details (implies lines)
* AccountPayableSalesTaxDetails (implies lines - only for Account Payable transaction)
* Summary (implies details)
* Addresses
* SummaryOnly (omit lines and details - reduces API response size)
* LinesOnly (omit details - reduces API response size)
* TaxDetailsByTaxType - Includes the aggregated tax, exempt tax, taxable and non-taxable for each tax type returned in the transaction summary.

### Security Policies

* This API requires one of the following user roles: AccountAdmin, AccountOperator, AccountUser, AvaTaxOnlyAccountAdmin, AvaTaxOnlyAccountUser, AvaTaxOnlyCompanyAdmin, AvaTaxOnlyCompanyUser, BatchServiceAdmin, CompanyAdmin, CompanyUser, CSPAdmin, CSPTester, ProStoresOperator, ReturnsOnlyAccountAdmin, ReturnsOnlyAccountUser, ReturnsOnlyCompanyAdmin, ReturnsOnlyCompanyUser, SiteAdmin, SSTAdmin, SystemAdmin, TechnicalSupportAdmin, TechnicalSupportUser.
* This API depends on the following active services:*Required* (all):  AvaTaxPro, BasicReturns.

## Parameters

| Name | Type | In | Required | Description |
|---|---|---|---|---|
| `id` | integer | path | Yes | The unique ID number of the transaction to retrieve |
| `$include` | string | query | No | Specifies objects to include in this fetch call |
| `X-Avalara-Client` | string | header | No | Identifies the software you are using to call this API.  For more information on the client header, see [Client Headers](https://developer.avalara.com/avatax/client-headers/) . |

## Responses

| Status | Description |
|---|---|
| 200 | Success |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |

<span style="color: rgb(224, 82, 0);">GetTransactionByCode</span></span></span>
## Retrieve a single transaction by code

`GET /api/v2/companies/{companyCode}/transactions/{transactionCode}`

**API:** AvaTax API
**Tag:** Transactions
**Operation ID:** GetTransactionByCode
**API Version:** v2
**Base URL:** https://sandbox-rest.avatax.com/

Source: https://developer.avalara.com/products/avatax/api/methods/Transactions/GetTransactionByCode/

## Description

Get the current transaction identified by this company code, transaction code, and document type.
            
A transaction is uniquely identified by `companyCode`, `code` (often called Transaction Code), and `documentType`.
            
For compatibility purposes, when this API finds multiple transactions with the same transaction code, and if you have not specified
the `type` parameter to this API, it will default to selecting the `SalesInvoices` transaction. To change this behavior, use the
optional `documentType` parameter to specify the specific document type you wish to find.
            
If this transaction was adjusted, the return value of this API will be the current transaction with this code.
            
You may specify one or more of the following values in the `$include` parameter to fetch additional nested data, using commas to separate multiple values:
            
* Lines
* Details (implies lines)
* AccountPayableSalesTaxDetails (implies lines - only for Account Payable transaction)
* Summary (implies details)
* Addresses
* SummaryOnly (omit lines and details - reduces API response size)
* LinesOnly (omit details - reduces API response size)
            
NOTE: If your companyCode or transactionCode contains any of these characters /, +, ? or a space please use the following encoding before making a request:
* Replace '/' with '\_-ava2f-\_'  For example: document/Code becomes document_-ava2f-_Code
* Replace '+' with '\_-ava2b-\_'  For example: document+Code becomes document_-ava2b-_Code
* Replace '?' with '\_-ava3f-\_'  For example: document?Code becomes document_-ava3f-_Code
* Replace '%' with '\_-ava25-\_'  For example: document%Code becomes document_-ava25-_Code
* Replace '#' with '\_-ava23-\_'  For example: document#Code becomes document_-ava23-_Code
* Replace ' ' with '%20'  For example: document Code becomes document%20Code

### Security Policies

* This API requires one of the following user roles: AccountAdmin, AccountOperator, AccountUser, AvaTaxOnlyAccountAdmin, AvaTaxOnlyAccountUser, AvaTaxOnlyCompanyAdmin, AvaTaxOnlyCompanyUser, BatchServiceAdmin, CompanyAdmin, CompanyUser, CSPAdmin, CSPTester, ProStoresOperator, ReturnsOnlyAccountAdmin, ReturnsOnlyAccountUser, ReturnsOnlyCompanyAdmin, ReturnsOnlyCompanyUser, SiteAdmin, SSTAdmin, SystemAdmin, TechnicalSupportAdmin, TechnicalSupportUser.
* This API depends on the following active services:*Required* (all):  AvaTaxPro, BasicReturns.

## Parameters

| Name | Type | In | Required | Description |
|---|---|---|---|---|
| `companyCode` | string | path | Yes | The company code of the company that recorded this transaction |
| `transactionCode` | string | path | Yes | The transaction code to retrieve |
| `documentType` | string | query | No | (Optional): The document type of the transaction to retrieve |
| `$include` | string | query | No | Specifies objects to include in this fetch call |
| `X-Avalara-Client` | string | header | No | Identifies the software you are using to call this API.  For more information on the client header, see [Client Headers](https://developer.avalara.com/avatax/client-headers/) . |

## Responses

| Status | Description |
|---|---|
| 200 | Success |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |

