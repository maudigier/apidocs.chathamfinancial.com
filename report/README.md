GET /report/{id}
=======

Returns the contents of the report file or the status of the report if it is not ready.

#### Example Request

```bash
curl https://api.chathamfinancial.com/report/12345 
	-H "Authorization: Bearer XXX" 
	-H "Accept: application/json"
```

#### Example Response

The status code of the response indicates the status of the request.

|  Status Code  | Description
| :-----------: | -----------
| 200           | Report is ready.
| 202           | Report is still generating.
| 400           | Parameter validation failed. Check the response body for details.
| 401           | Missing, invalid, expired or revoked access token.
| 404           | Report is invalid. Check the value of the `id` parameter.
| 500           | Report generation failed. Try again or contact support if you continue to receive this response.

<br />

POST /report/portfolio
=======

Queues a new report job for your entire portfolio of transactions.

#### Example Request

```bash
curl https://api.chathamfinancial.com/report/portfolio 
	-X POST
	-H "Authorization: Bearer XXX" 
	-H "Accept: application/json" 
	-H "Content-Type: application/json" 
	-d '{ "asofdate": "2013-01-31", "fromdate": "2013-01-01", "todate": "2013-01-31", "datagroupings": 1 }'
```

| Parameter     | Type      |  Required  | Description                      |
| ------------- | --------- | :--------: | -------------------------------- |
| AsOfDate      | `string`  | Yes        | A date in the format YYYY-MM-DD. |
| FromDate      | `string`  | Yes        | A date in the format YYYY-MM-DD. |
| ToDate        | `string`  | Yes        | A date in the format YYYY-MM-DD. |
| DataGroupings | `integer` | Yes        | A bitmask of one or more data groups. 1 - Economics, 2 - Schedule, 3 - Forecasting, 4 - Valuations |

#### Example Response

```json
{
	"JobId": 54321
}
```

The status code of the response indicates the status of the request.

|  Status Code  | Description
| :-----------: | -----------
| 200           | Report is ready.
| 400           | Parameter validation failed. Check the response body for details.
| 401           | Missing, invalid, expired or revoked access token.
| 500           | Report generation failed. Try again or contact support if you continue to receive this response.