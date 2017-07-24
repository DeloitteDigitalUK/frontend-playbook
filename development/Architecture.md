# Front-end Architecture

## Error handling

### Barricades
Barricades are a damage-containment strategy. The reason is similar to that for having isolated compartments in the hull of a ship.
If the ship runs into an iceberg and pops open the hull, that compartment is shut off and the rest of the ship isn't affected.  

One way to barricade for defensive programming purposes is to designate certain interfaces as boundaries to "safe" areas.  

In a front-end application it is important to check data crossing the boundaries of a safe area (e.g. an API call payload) for validity, and respond sensibly if the data isn't valid. The easiest way to do this is usually by sanitizing external data as it arrives, but data often needs to be sanitized at more than one level, so multiple levels of sterilization are sometimes required.

Incoming payload at runtime can be validated against a defined JSONSchema.  

For example, we can use a library [AJV](https://www.npmjs.com/package/ajv) to validate against a [JSONSchema](https://www.npmjs.com/package/jsonschema)

```javascript
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
};

const isValid = ajv.validate(schema, data); // => true

if (!isValid) {
    console.log(ajv.errors);
}
```
  
The use of barricades makes the distinction between assertions and error handling clean-cut. Routines that are outside the barricade should use error handling because it isn't safe to make any assumptions about the data. Routines inside the barricade should use assertions, because the data passed to them is supposed to be sanitized before it's passed across the barricade. If one of the routines inside the barricade detects bad data, that's an error in the program rather than an error in the data.

The use of barricades ais an architecture-level decision on how to handle errors.
  
