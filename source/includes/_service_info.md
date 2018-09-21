

# Service Information
## Getting stats
> Example Request

```shell
curl --request GET \
  --url http://localhost:7791/service/stats/{service_name}
```

```javascript
var request = require("request");

var options = { method: 'GET', url: 'http://localhost:7791/service/stats/{service_name}' };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```

```go
package main

import (
	"fmt"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "http://localhost:7791/service/stats/{service_name}"

	req, _ := http.NewRequest("GET", url, nil)

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
	"message": "Got service status",
	"success": true,
	"error": "",
	"response": {
		"controld": {
			"running": false,
			"pid": 0,
			"environment_vars": null,
			"executable_location": ""
		},
		"networkd": {
			"running": true,
			"pid": 45907,
			"environment_vars": [
				"GLADIUSBASE=/home/alex/.config/gladius"
			],
			"executable_location": "/usr/local/bin/gladius-networkd"
		}
	},
	"endpoint": "/service/stats/{service_name}"
}
```


### HTTP Request

`GET http://localhost:7791/service/stats/{service_name}`


### URL Parameters

Parameter | Description
--------- | -----------
service_name | The name of the service to get stats of.
