# Check if string/file contents are valid JSON

## Overview

Basic action to validate if input file contents, or input string are valid JSON.

## Usage

### Check if file content is valid JSON

Possible use case might be to validate configuration updates/edits to a JSON file when a PR is raised.

#### Example when input file contains *valid* JSON

Filename (all valid JSON): `${{ github.workspace }}/config-file.json`

```json
{
    "example_meta": [
        {
            "meta_no": "57",
            "meta_status": "active",
            "meta_suburb": {
                "name": "random_suburb",
                "zip": "012012"
            }
        }
    ]
}
```

Include step to validate contents of file `${{ github.workspace }}/config-file.json`.

```yaml
...
...
on:
  pull_request:
...

jobs:
  ...
  ...
    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: JSON string/file validator
        uses: tonys-code-base/json-check-action@v1.0.0
        id: json-file-chk
        with:
          json-file-path: ${{ github.workspace }}/config-file.json
```

output:

```
Run tonys-code-base/json-check-action@v1.0.0
  with:
    json-file-path: /runner/_work/***/***/config-file.json

Successfully parsed JSON file: 
/runner/_work/***/***/config-file.json
```

#### When input file contains *invalid* JSON

Same file but with invalid JSON: `${{ github.workspace }}/config-file.json`

```json
{
    "example_meta": [
        {
            "meta_no": "57",
            "meta_status": "active",
            "meta_suburb": {
                "name": "random_suburb",
            }
        }
    ]
}
```

sample workflow output:

```bash
Run tonys-code-base/json-check-action@v1.0.0
  with:
    json-file-path: /runner/_work/***/***/config-file.json

parse error: Expected another key-value pair at line 8, column 13
Error: Process completed with exit code 4.
```

### Using the action to validate JSON strings

```yaml
...
...

jobs:
  ...
  ...
    steps:
      - name: JSON string/file validator
        uses: tonys-code-base/json-check-action@v1.0.0
        id: json-str-chk
        with:
          json-string: >-
            {
              "example_meta": [
                  {
                      "meta_no": "57",
                      "meta_status": "active",
                      "meta_suburb": {
                          "name": "random_suburb",
                          "zip": "012012"
                      }
                  }
              ]
            }
```

Output:

```bash
0s
Run tonys-code-base/json-check-action@v1.0.0

Successfully parsed JSON string: 
{
  "example_meta": [
      {
          "meta_no": "57",
          "meta_status": "active",
          "meta_suburb": {
              "name": "random_suburb",
              "zip": "012012"
          }
      }
  ]
}
```

