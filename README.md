# Payload Injector

## Overview

**Payload Injector** is a Python module designed for modifying HTTP requests by injecting payloads into various parameters. It is useful for penetration testing, security research, and debugging web applications.

## Features

- Identifies injection points in **path**, **query parameters**, **request body**, **headers**, and **cookies**.
- Supports payload injection into:
  - URL query parameters
  - Form-encoded and JSON request bodies
  - Multipart form data (including file names)
  - HTTP headers and cookies
- Allows modifying the HTTP request method.
- Detects available injection points dynamically.

## Installation

Clone the repository:

```sh
git clone https://github.com/yourusername/payload-injector.git
cd payload-injector
```

## Usage

### Initializing the Injector

```python
from payload_injector import PayloadInjector


# Assume `http_request` is an object representing an HTTP request.
injector = PayloadInjector(http_request)
```

### Finding Injection Points

```python
injection_points = injector.find_injection_points()
print(injection_points)
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
