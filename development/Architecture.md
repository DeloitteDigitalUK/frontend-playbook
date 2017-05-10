# Front-end Architecture

## Barricades
Barricades are a damage-containment strategy. The reason is similar to that for having isolated compartments in the hull of a ship.
If the ship runs into an iceberg and pops open the hull, that compartment is shut off and the rest of the ship isn't affected.  

One way to barricade for defensive programming purposes is to designate certain interfaces as boundaries to "safe" areas.  

In a front-end application it is important to check data crossing the boundaries of a safe area (e.g. an API call payload) for validity, 
and respond sensibly if the data isn't valid.  

Incoming payload at runtime can be validated against a defined JSONSchema.  

For example, we can use a library [AJV](https://www.npmjs.com/package/ajv) to validate against a [JSONSchema](https://www.npmjs.com/package/jsonschema)

```
import Ajv from 'ajv';

const ajv = new Ajv();

const schema = {
    "id": "/SimpleAddress",
    "type": "object",
    "properties": {
      "country": {"type": "string"},
      "city": {"type": "string"}
    },
    "required": ["country"]
  };

const data = {
  country: 'United Kingdom'
}

const isValid = ajv.validate(schema, data); // => true

if (!isValid) {
    console.log(ajv.errors);
}
```
