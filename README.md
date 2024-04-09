# NovelAI OpenAPI Spec
This is the NovelAI OpenAPI Spec in JSON format with manual fixes to allow for automatic compilation

## Usage
```bash
git clone https://github.com/nai-tools/nai-openapi
cd nai-openapi

openapi-generator-cli generate -i ./nai-openapi.json -g <language> -o <output dir>

# Generate API for Go
openapi-generator-cli generate -i ./nai-openapi.json -g go -o go-api/
# Generate API for Python
openapi-generator-cli generate -i ./nai-openapi.json -g python -o python-api/
```

## Notes on Modifications

### -attribute components.schemas.BindSubscriptionRequest.default is unexpected
```js
// [(JSON Ommitted)]
"BindSubscriptionRequest": {
    "type": "object",
    "properties": {
        // [(JSON Ommitted)]
        "confirmedReplace": {
            "type": "object", // <- This type (changed to boolean)
            "default": false, // <- Does not match this default value
            "description": "Whether the user confirmed replacing the subscription"
        },
        "confirmedIgnore": {
            "type": "object", // <- This type (changed to boolean)
            "default": false, // <- Does not match this default value
            "description": "Whether the user confirmed ignoring the subscription"
        }
    },
    // [(JSON Ommitted)]
}
// [(JSON Ommitted)]
```
The above issue is solved in this repository by changing the type of `confirmedReplace` & `confirmedIgnore` to `boolean`.
