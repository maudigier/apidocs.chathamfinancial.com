GET /report/transactions
=======

Returns reporting data pertaining to transactions

### Common API Components

[See Common API Components](../../../../blob/master/Common.md)

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
| ProductType | Swap | Type of financial instrument of which the transaction consists. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ProductDescription | Sells CNY/Buys USD Forward | Description of financial instrument of which the transaction consists (typically more detailed than 'Product'). | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Description | Hedge of anticipated cash flow | Custom description of the transaction. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| Alias | 2013-03 CNY 8.59mm Sells CNY/Buys USD Forward Natixis | Descriptive nickname for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| HedgedItem | Floating Rate Term Loan A | Description of the item being hedged. This field is particularly relevant if hedge accounting is being applied to the trade. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | Yes | Yes | Yes | Yes | Yes
| FXCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions. | null | null | null | null | Yes | Yes | Yes | Yes | Yes
| StrikeRateDescription | 58.00 - 52.825 USD-INR | Description of the strike price(s) or strike rate(s) for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| IndexDescription | 3 mo. EUR-Euribor-Telerate     | Description of the underlying index or rate(s) for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| SpreadDescription | 300.00 bps | Description of the spread(s) applied to the index for the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | null | null | null | null
| NotionalCurrency | USD | Currency in which the 'DescriptiveNotional' is reported. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| NotionalAmountDescription | 10000000 | Description of the notional amount(s) of the transaction generated by Chatham upon loading. | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes
| ClientLegalEntity | MSREF VII HEDGING, L.P. | Legal entity related to Chatham's client that is party to the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| CounterpartyLegalEntity | Natixis | Legal entity that is the counterparty to Chatham's client in the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TradeDate | 2013-03-12 08:30:00 | Date and time when the trade was executed. Time is specified as 00:00 if it was not input. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| TradeDateTimezone | UTC-5:00 | Timezone with respect to which 'TradeDate' is reported. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| PremiumCurrency | USD | Currency in which the premium is paid. | null | yes | yes | yes | null | null | null | yes | yes
| PremiumAmount | -400000 | Premium amount paid or received by 'ClientLegalEntity'. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. | null | yes | yes | yes | null | null | null | yes | yes
| PremiumPaymentDate | 2013-10-12 | Date the 'PremiumAmount' was due to be paid. | null | yes | yes | yes | null | null | null | yes | yes
| SwaptionDirection | Buys | Indicates whether the client is buying or selling the swaption. | null | null | null | yes | null | null | null | null | null
| OptionExpirationDate | 2013-11-25 16:00:00 | For option products, the date and time when the option expires. Returns null for non-option products. | null | yes | yes | yes | null | null | null | yes | yes
| SettlementType | Deliverable | States whether the derivative contract is deliverable. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| SettlementDate | 2013-05-25 | Date when the executed option is settled. | null | null | null | null | null | yes | yes | yes | yes
| ScheduleType | Bullet | Payment Schedule Type. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| EffectiveDate | 2013-10-15 | Date the executed trade is effective. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| MaturityDate | 2014-11-30 | Date which is the end of the lifespan for the interest bearing security. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1Direction | Pays Sells | Indicates whether the client buys/recieves or selles/recieves the product for leg 1 of the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2Direction | Receives Buys | Indicates whether the client buys/recieves or selles/recieves the product for leg 2 of the transaction. | yes | null | yes | yes | yes | null | null | null | yes
| Leg1Type | Fixed Cap Put | Indicates for IR trades if leg 1 of the transaction is fixed or floating.  For FX trades, indicates the currency code and in the case of FX options, put or call. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2Type | Floating Floor Call | Indicates for IR trades if leg 2 of the transaction is fixed or floating.  For FX trades, indicates the currency code and in the case of FX options, put or call. | yes | null | yes | yes | yes | null | null | null | yes
| Leg1FxOptionStyle | European | The specific type of FX option used for leg 1 of the transaction. | null | null | null | null | null | null | null | yes | yes
| Leg2FxOptionStyle | European | The specific type of FX option used for leg 1 of the transaction. | null | null | null | null | null | null | null | yes | yes
| Leg1PaymentFrequency | Monthly | For interest rate products, the payment frequency of the first leg of the transaction. | yes | yes | yes | yes | yes | null | null | null | null
| Leg2PaymentFrequency | Semi-annually | For interest rate products, the payment frequency of the second leg of the transaction. | yes | yes | yes | yes | yes | null | null | null | null
| Leg1Currency | USD | Same as Notional Currency. | null | null | null | null | yes | yes | yes | yes | yes
| Leg2Currency | GBP | Home Currency, only applies to FX trades and cross currency swaps. | null | null | null | null | yes | yes | yes | yes | yes
| Leg1NotionalAmount | 100000 | The notional amount of the corresponding currency.  In an FX trade, this is the exchange amount. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2NotionalAmount | 160000 | The notional amount of the corresponding currency.  In an FX trade, this is the exchange amount. | yes | null | yes | yes | yes | null | null | null | yes
| Leg1StrikeRate | 98.65 | The agreed upon strike rate, either interest rate or foreign exchange rate, relevant for leg 1 of the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2StrikeRate | 1.3437 | The agreed upon strike rate, either interest rate or foreign exchange rate, relevant for leg 2 of the transaction. | yes | null | yes | yes | yes | null | null | null | yes
| Leg1IndexName | USD-PEN | Name of the index being used for leg 1 of the  transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg2IndexName | 3 mo. USD-LIBOR-BBA | Name of the index being used for leg 2 of the  transaction. | yes | null | yes | yes | yes | null | null | null | yes
| Leg1SpreadOverIndex | 0.0375 | The spread to the index being used for leg 1 of the transaction (should return blank if leg is fixed). | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2SpreadOverIndex | 0.025 | The spread to the index being used for leg 2 of the transaction (should return blank if leg is fixed). | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1DayCountFraction | Act/365 Fixed |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1PeriodEndBusinessDayConvention | Modified Following |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1PaymentBusinessDayConvention | Modified Following |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1NotionalCurrency | PEN |  | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1FxCurrency | PEN |  | null | null | null | null | null | yes | yes | yes | yes
| Leg1FxCurrencyAmount | -176680.58 |  | null | null | null | null | null | yes | yes | yes | yes
| Leg1HomeCurrency | USD |  | null | null | null | null | null | yes | yes | yes | yes
| Leg1HomeCurrencyAmount | 62398.23 |  | null | null | null | null | null | yes | yes | yes | yes
| Leg2DayCountFraction | Act/365 Fixed |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2PeriodEndBusinessDayConvention | Modified Following |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2PaymentBusinessDayConvention | Modified Following |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2NotionalCurrency | INR |  | yes | null | yes | yes | yes | null | null | null | yes
| Leg2FxCurrency | INR |  | null | null | null | null | null | null | null | null | yes
| Leg2FxCurrencyAmount | -200735000 |  | null | null | null | null | null | null | null | null | yes
| Leg2HomeCurrency | USD |  | null | null | null | null | null | null | null | null | yes
| Leg2HomeCurrencyAmount | 3800000 |  | null | null | null | null | null | null | null | null | yes
| Leg1CurrentPeriodNotionalCurrency | EUR | The current period notional currency for leg 1 of the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1CurrentPeriodNotionalAmount | 9585821.05 | The current period notional amount for leg 1 of the transaction. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| Leg1CurrentPeriodFixedRate | 0.035 | For IR trades, the current period fixed rate for leg 1 of the transaction. | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1CurrentPeriodFloatingRate | 0.00227 | Index rate applicable to the current period for leg 1 of the transaction. | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1CurrentPeriodFloatingRateFixingDate |  | For IR trades, the current period fixed rate for leg 1 of the transaction. | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1CurrentPeriodFloatingRateResetDate |  |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1CurrentPeriodSpread | 0.0655 |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1CurrentPeriodStartDate |  |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1CurrentPeriodEndDate |  |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg1CurrentPeriodPaymentDate |  |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodNotionalCurrency | USD | The current period notional currency for leg 2 of the transaction. | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodNotionalAmount | 33800000 | The current period notional amount for leg 2 of the transaction. | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodFixedRate | NULL | For IR trades, the current period fixed rate for leg 2 of the transaction. | null | null | yes | null | yes | null | null | null | yes
| Leg2CurrentPeriodFloatingRate | 0.0058875 | Index rate applicable to the current period for leg 2 of the transaction. | null | null | yes | null | yes | null | null | null | yes
| Leg2CurrentPeriodFloatingRateFixingDate |  |  | null | null | yes | null | yes | null | null | null | yes
| Leg2CurrentPeriodFloatingRateResetDate |  |  | null | null | yes | null | yes | null | null | null | yes
| Leg2CurrentPeriodSpread | 0.0145 |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodStartDate |  |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodEndDate |  |  | yes | yes | yes | yes | yes | null | null | null | yes
| Leg2CurrentPeriodPaymentDate |  |  | yes | yes | yes | yes | yes | null | null | null | yes
| FxSpotRateCurrencyPair | GBP-AUD |  | null | null | null | null | yes | yes | yes | yes | yes
| FxSpotRateReportStart | 1.69605 |  | null | null | null | null | yes | yes | yes | yes | yes
| FxSpotRateReportEnd | 1.7953 |  | null | null | null | null | yes | yes | yes | yes | yes
| Status | Active | Current status of the trade, typically active, matured, or terminated. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| NextPaymentDate | 3/27/2014  12:00:00 AM | Date of next due payment. | yes | yes | yes | yes | yes | null | null | null | yes
| UserDefinedField1 | MSREF7 | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField2 | GBP HEDGE | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField3 | Fund Level Hedge | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField4 | UK | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField5 | CFMSSANDB2013032901 | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField6 | NULL | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField7 | NULL | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField8 | Europe | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField9 | NULL | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
| UserDefinedField10 | NULL | User defined custom field. | yes | yes | yes | yes | yes | yes | yes | yes | yes
