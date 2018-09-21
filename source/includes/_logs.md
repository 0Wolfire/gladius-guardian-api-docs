# Logs

## Get up to the last thousand lines of logs from all services

> Example request

```shell
curl --request GET \
  --url http://localhost:7791/service/logs
```

```javascript
var request = require("request");

var options = { method: 'GET', url: 'http://localhost:7791/service/logs' };

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

	url := "http://localhost:7791/service/logs"

	req, _ := http.NewRequest("GET", url, nil)

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

> Response 200

```json
{
	"message": "Got logs",
	"success": true,
	"error": "",
	"response": {
		"controld": [
			"Starting API at http://localhost:3001"
		],
		"networkd": [
			"Loading config",
			"2018/09/21 17:58:13 Loading website: demo.gladius.io",
			"Starting...",
			"2018/09/21 17:58:13 Loaded route: test",
			"Started RPC server and HTTP server.",
			"2018/09/21 17:58:13 Loaded route: test (another copy)",
			"2018/09/21 17:58:13 Loaded route: test (copy)",
			"2018/09/21 17:58:13 Loading website: test.gladius.io",
			"2018/09/21 17:58:13 Loaded route: test"
		]
	},
	"endpoint": "/service/logs"
}
```

### HTTP Request

`GET http://localhost:7791/service/logs`
