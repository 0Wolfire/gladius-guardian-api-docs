# Logs

## Get up to the last thousand lines of logs from all services
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

### HTTP Request

`GET http://localhost:7791/service/logs`
