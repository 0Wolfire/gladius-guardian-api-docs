# Managing services

## Start/Stop a service
> Example Request

```shell
curl --request PUT \
  --url http://localhost:7791/service/set_state/{service_name} \
  --header 'content-type: application/json' \
  --data '{"running": true,	"environment_vars" = ["GLADIUSBASE=/your/base/here"]}'
```

```javascript
var request = require("request");

var options = { method: 'PUT',
  url: 'http://localhost:7791/service/set_state/controld',
  headers: { 'content-type': 'application/json' },
  body: '{\n\t"running": true\n\t"environment_vars" = ["GLADIUSBASE=/your/base/here"]\n}' };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```
```go
package main

import (
	"fmt"
	"strings"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "http://localhost:7791/service/set_state/controld"

	payload := strings.NewReader("{\n\t\"running\": true\n\t\"environment_vars\" = [\"GLADIUSBASE=/your/base/here\"]\n}")

	req, _ := http.NewRequest("PUT", url, payload)

	req.Header.Add("content-type", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```
> Response (200)

```json
{
	"message": "Attempted to start service, check logs to make sure it didn't fail after timeout",
	"success": true,
	"error": "",
	"response": {
		"controld": {
			"running": true,
			"pid": 100678,
			"environment_vars": [
				"GLADIUSBASE=/home/alex/.config/gladius"
			],
			"executable_location": "/usr/local/bin/gladius-controld"
		},
		"networkd": {
			"running": false,
			"pid": 0,
			"environment_vars": null,
			"executable_location": ""
		}
	},
	"endpoint": "/service/set_state/controld"
}
```

### HTTP Request

`PUT http://localhost:7791/service/set_state/{service_name}`

### URL Parameters

Parameter | Description
--------- | -----------
service_name | The name of the service to change run state.


<aside class="notice">
You can change <code>service_name</code> with <code>all</code> to control all
registered services.
</aside>


### JSON Body Parameters

Parameter | Description | Example
--------- | -----------  | -------
"environment_vars" | Optional environment_vars for starting a service | ["GLADIUSBASE=/your/base/here"]
"running" | The desired run state of the service | true/false
