GET /reports/transactions
=======

Returns reporting data pertaining to transactions

### Common API Components

[See Common API Components](../blob/master/Common.md)

### Example Request

```bash
curl https://api.chathamfinancial.com/report/transactions?fromdate=2013-07-01&todate=2013-09-30&offset=0
	-X GET
	-H "Authorization: Bearer XXX"
    -H "X-Fields: items(Id, EffectiveDate, Notional, NotionalCurrency)"
```

### Example Response

```json
{
    "Paging": {
        "Limit": 500,
        "Offset": 0,
        "TotalRecords": 2
    },
    "Items": [{
            "Id": "CFSponsor20110930",
            "EffectiveDate": "2011-09-30",
            "Notional": 30000000,
    	    "NotionalCurrency": "USD"	
		},
        {
	    	"Id": "CFSponsor201311031",
    		"EffectiveDate": "2011-11-31",
    		"Notional": 250000000,
    		"NotionalCurrency": "EUR"	
		}
	]	
}
```

### Request Query String Parameters

| Parameter     | Type      |  Required  | Description                      |
| ------------- | --------- | :--------: | -------------------------------- |
| fromdate      | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |
| todate        | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |


### Response Codes

|  Status Code  | Description
| :-----------: | -----------
| 200           | The transaction data is returned.
| 400           | Parameter validation failed. Check the response body for details. 
| | Examples: 
| | - Invalid Column name  
| | - From Date is not in the specified Date format
| | - To Date is not in the specified Date format
| 401           | Missing, invalid, expired or revoked access token.
| 500           | Transaction data gathering failed. Try again or contact support if you continue to receive this response.



### Supported Transaction Data Fields

<br><br>

| Field Name    | Example Value  | Description    | Swap   | Cap/Floor   | Collar | Swaption    | Cross Currency Swap | FX Spot | FX Fwd | FX Option | FX Collar
| :-----------: | -------------- | -------------- | ------ | ----------- | ------ | ----------- | ------------------- | ------- | ------ | --------- | -------------- 
| ReportStartDate | 2013-10-31 | The start date specified for the report. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ReportEndDate | 2013-11-30 | The end date specified for the report. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ReportCreationTimestamp | 2013-11-25 16:00 | Date and time when the report was created (run). | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| TradeInputDate | 2013-11-06 | Date that the trade was loaded into ChathamDirect. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| TradeInputUser | Joe Smith | Name of user that input the trade into ChathamDirect. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ConfirmCheckDate | 2013-11-08 | Date when the Confirm Check action in ChathamDirect was designated as complete for this trade  – will return null if not confirmed. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ConfirmCheckUser | Joe Smith | Name of user that designated the Confirm Check action in ChathamDirect as complete – should return null if not confirmed.  | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| LastModicationDate | 2013-11-13 | Date when a material economic or descriptive field was last modified. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| LastModificationUser | Joe Smith | Name of the user that made the last modification to a material economic of descriptive field. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ChathamReferenceNumber | CFDEMOCORP2011120510 | Unique reference number  assigned to the transaction by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ClientReferenceNumber | 10101010AB | Reference number assigned to the transaction by the client. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| CounterpartyReferenceNumber | 10101010AB | Reference number assigned to the transaction by the dealer counterparty. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| LoanReferenceNumber | 10101010AB | Reference number of the underlying loan related to the transaction (if applicable). | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Portfolio1 | My Derivative Portfolio | Optional custom name used to group a set of transactions. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Portfolio2 | My Derivative Portfolio | Optional custom name used to group a set of transactions. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Portfolio3 | My Derivative Portfolio | Optional custom name used to group a set of transactions. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| DescriptiveProduct | Sells CNY/Buys USD Forward | Description of financial instrument of which the transaction consists (typically more detailed than 'Product'). | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Product | Swap | Type of financial instrument of which the transaction consists. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Description | Hedge of anticipated cash flow | Custom description of the transaction. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Alias | 2013-03 CNY 8.59mm Sells CNY/Buys USD Forward Natixis | Descriptive nickname for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| HedgedItem | Floating Rate Term Loan A | Description of the item being hedged. This field is particularly relevant if hedge accounting is being applied to the trade. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | Yes | Yes | Yes | Yes | Yes
| ForeignCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | Yes | Yes | Yes | Yes | Yes
| DescriptiveStrikeRate | 58.00 - 52.825 USD-INR | Description of the strike price(s) or strike rate(s) for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| DescriptiveIndex | 3 mo. EUR-Euribor-Telerate     | Description of the underlying index or rate(s) for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| DescriptiveSpread | 300.00 bps | Description of the spread(s) applied to the index for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | null | null | null | null
| DescriptiveNotionalCurrency | USD | Currency in which the 'DescriptiveNotional' is reported. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| DescriptiveNotionalAmount | 10000000 | Description of the notional amount(s) of the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
