# Check if string/file contents are valid JSON

## Overview

Basic action to validate if input file contents, or input string are valid JSON.

## Usage

### Check if string is valid JSON

```yaml
...
...

jobs:
  ...
  ...
    steps:
      - name: Check if string is valid json
        uses: tonys-code-base/json-check-action@v0.1.0-alpha
        id: json-str-chk
        with:
          json-string: >-
            {
              "mykeys": {
                  "name": "somename",
                  "surname": "somesurname"
              }
            }
```



### Check if file content is valid JSON

Validate content of file `${{ github.workspace }}/test-file.json`.

```yaml
...
...

jobs:
  ...
  ...
    steps:
      - name: Check input file contains valid json
        uses: tonys-code-base/json-check-action@v0.1.0-alpha
        id: json-file-chk
        with:
          json-file-path: ${{ github.workspace }}/test-file.json
```

