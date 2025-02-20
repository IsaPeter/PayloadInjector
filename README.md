# Payload Injector

## Overview

**Payload Injector** is a Python module designed for modifying HTTP requests by injecting payloads into various parameters. It is useful for penetration testing, security research, and debugging web applications.

The library relies on the followin HTTPRequest library: [https://github.com/IsaPeter/httplib.git](https://github.com/IsaPeter/httplib.git)

## Features

- Identifies injection points in **path**, **query parameters**, **request body**, **headers**, and **cookies**.
- Supports payload injection into:
  - URL query parameters
  - Form-encoded and JSON request bodies
  - Multipart form data (including file names)
  - HTTP headers and cookies
- Allows modifying the HTTP request method.
- Detects available injection points dynamically.


## Usage

**Example HTTP Request**

```http
GET /htmli_get.php?firstname=asd&lastname=asd&form=submit HTTP/1.1
Host: 127.0.0.1:8888
sec-ch-ua: "Chromium";v="121", "Not A(Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Linux"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.6167.85 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://127.0.0.1:8888/htmli_get.php
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: security_level=0; PHPSESSID=vmen7h1bdbl78umenh1t0qiko3
Connection: close
```

### Initializing the Injector

```python
from payload_injector import PayloadInjector
from httplib import HTTPRequest

http_request = HTTPRequest(raw_http_request_data)

# Assume `http_request` is an object representing an HTTP request.
injector = PayloadInjector(http_request)
```

### Finding Injection Points

```python
injection_points = injector.find_injection_points()
print(injection_points)
```

The result injection points in JSON format:

```json
{
     "path": [
          "/htmli_get.php",
          "htmli_get.php"
     ],
     "query": [
          "firstname",
          "lastname",
          "form"
     ],
     "body": [],
     "headers": [
          "Host",
          "sec-ch-ua",
          "sec-ch-ua-mobile",
          "sec-ch-ua-platform",
          "Upgrade-Insecure-Requests",
          "User-Agent",
          "Accept",
          "Sec-Fetch-Site",
          "Sec-Fetch-Mode",
          "Sec-Fetch-User",
          "Sec-Fetch-Dest",
          "Referer",
          "Accept-Encoding",
          "Accept-Language",
          "Cookie",
          "Connection"
     ],
     "cookies": [
          "security_level",
          "PHPSESSID"
     ]
}
```

### Injecting a Payload

```python
injector.inject_payload(target="query", key="param", payload="InjectedValue")
```

### Modifying HTTP Method

```python
injector.set_method("POST")
```

### Getting Available Injection Points

```python
available_points = injector.get_available_injection_points()
print(available_points)
```


## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Disclaimer
This tool is intended for educational and ethical penetration testing purposes only. Unauthorized use against systems without explicit permission is strictly prohibited.
