GET /report/{id}
=======

Returns the contents of the report file or the status of the report if it is not ready.

##### Example Request

```bash
curl https://api.chathamfinancial.com/report/12345 
	-H "Authorization: Bearer XXX" 
	-H "Accept: application/json"
```

##### Example Response

The status code of the response indicates the status of the request.

<table cellpadding="8" border="1">
	<tr>
		<th align="left" nowrap>Status Code</th>
		<th align="left" nowrap>Description</th>
	</tr>
	<tr>
		<td>200</td>
		<td>Report is ready</td>
	</tr>
	<tr>
		<td>202</td>
		<td>Report is still generating</td>
	</tr>
	<tr>
		<td>400</td>
		<td>Parameter validation failed. Check the response body for details.</td>
	</tr>
	<tr>
		<td>401</td>
		<td>Missing, invalid, expired or revoked access token.</td>
	</tr>
	<tr>
		<td>404</td>
		<td>Report is invalid. Check the value of the id parameter.</td>
	</tr>
	<tr>
		<td>500</td>
		<td>Report generation failed. Try again, or contact Chatham support if you continue to receive this response.</td>
	</tr>
</table>

POST /report/portfolio
=======

Queues a new report job for your entire portfolio of transactions.

##### Example Request

```bash
curl https://api.chathamfinancial.com/report/portfolio 
	-X POST
	-H "Authorization: Bearer XXX" 
	-H "Accept: application/json" 
	-H "Content-Type: application/json" 
	-d '{ "asofdate": "2013-01-31", "fromdate": "2013-01-01", "todate": "2013-01-31", "datagroupings": 1 }'
```

##### Example Response

```json
{
	"JobId": 54321
}
```

The status code of the response indicates the status of the request.

<table cellpadding="8" border="1">
	<tr>
		<th align="left" nowrap>Status Code</th>
		<th align="left" nowrap>Description</th>
	</tr>
	<tr>
		<td>200</td>
		<td>The report job has been successfully queued</td>
	</tr>
	<tr>
		<td>400</td>
		<td>Parameter validation failed. Check the response body for details.</td>
	</tr>
	<tr>
		<td>401</td>
		<td>Missing, invalid, expired or revoked access token.</td>
	</tr>
	<tr>
		<td>500</td>
		<td>Failed to queue the report job. Try again, or contact Chatham support if you continue to receive this response.</td>
	</tr>
</table>