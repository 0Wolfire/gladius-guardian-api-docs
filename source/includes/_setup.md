# Setup
## Set startup timeout
> Example request

```shell
curl --request POST \
  --url http://localhost:7791/service/set_timeout \
  --header 'content-type: application/json' \
  --data '{"timeout": 3}'
```

```javascript
var request = require("request");

var options = { method: 'POST',
  url: 'http://localhost:7791/service/set_timeout',
  headers: { 'content-type': 'application/json' },
  body: { timeout: 3 },
  json: true };

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

	url := "http://localhost:7791/service/set_timeout"

	payload := strings.NewReader("{\n\t\"timeout\": 3\n}")

	req, _ := http.NewRequest("POST", url, payload)

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
	"message": "Set timeout",
	"success": true,
	"error": "",
	"response": {
		"timeout": 3
	},
	"endpoint": "/service/set_timeout"
}
```
This endpoint sets the startup timeout for services. This is required before
services can be started, as it's how we check for an fast exit of the
service. If the service exits before the timeout is reached, this will return
an error.

### HTTP Request

`POST http://localhost:7791/service/set_timeout`
