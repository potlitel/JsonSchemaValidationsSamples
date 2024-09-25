# JSON Schema - Validations samples

<div id="top"></div>

## Table of Contents:

- ✨[About](#✨about)
- 📃[Validations samples](#📃validations-samples)
  - 💠[Required string prop](#💠required-string-prop)  
  - 💠[Required string prop with pattern](#💠required-string-prop-with-pattern)
  - 💠[boolean](#💠boolean)  
  - 💠[minLength-maxLength](#💠minlength-maxlength)
  - 💠[number](#💠number)  
  - 💠[minimum-maximum](#💠minimum-maximum)
  - 💠[date](#💠date)  
  - 💠[date-time](#💠date-time)
  - 💠[arrays](#💠arrays)  
  - 💠[arrays-prefixItems](#💠arrays-prefixitems)
  - 💠[defs](#💠defs)  
  - 💠[refs](#💠refs)
  - 💠[External refs](#💠external-refs)  
  - 💠[arrays and defs combinations](#💠arrays-and-defs-combinations)
  - 💠[defs with enums](#💠defs-with-enums)  
  - 💠[strings with enums](#💠strings-with-enums)
  - 💠[array with enums](#💠array-with-enums)  
  - 💠[Reusing common types](#💠reusing-common-types)
  - 💠[object type](#💠object-type)  
  - 💠[allOf](#💠allof)
  - 💠[oneOf](#💠oneof)
  - 💠[anyOf](#💠anyof)  
  - 💠[Third party solutions](#💠third-party-solutions)
- 📚[Acknowledgments](#📚acknowledgments)

## ✨About

JSON Schema is a declarative language for annotating and validating JSON documents' structure, constraints, and data types. It provides a way to standardize and define expectations for JSON data.

>[!NOTE]
   >
   >The JSON Schema team recommends using draft 7 or later. The current version is 2020-12! The previous version was 2019-09.

All the examples listed below have the same structure but for the sake of brevity, we will only be showing the code snippet corresponding to the validation segment:

```json

{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://example.com/product.schema.json",
  "title": "Your title",
  "description": "Your description",
  "type": "object",
  "additionalProperties": false,
  "required": [ ... ],
  "properties": {
    "prop1": {
    },
    "prop2": {
    },
    "prop3": {
    },
    "propn": {
    }
  },
  "definitions": {
    "definition-1": {
    },
    "definition-2": {
    },
    "definition-n": {
    }
}

```

## 📃Validations samples

### 💠Required string prop

```json
{
...// MORE CODE OMITTED FOR BREVITY
"required": [ "FirstName" ],
"properties": {
"FirstName": {
      "type": "string"
    },
},
...// MORE CODE OMITTED FOR BREVITY
}
```
<p align="right"><a href="#top">☝</a></p>

### 💠Required string prop with pattern

```json
{
...// MORE CODE OMITTED FOR BREVITY
"required": [ "telephone_number" ],
"properties": {
        "telephone_number": {
            "type": "string",
            "pattern": "^(\\([0-9]{3}\\))?[0-9]{3}-[0-9]{4}$" //"555-1212", "(888)555-1212", "(888)555-1212 ext. 532"
            },
},
...// MORE CODE OMITTED FOR BREVITY
}
```
<p align="right"><a href="#top">☝</a></p>

### 💠boolean

```json
{
...// MORE CODE OMITTED FOR BREVITY
"properties": {
        "ignitionStatus": {
          "type": "boolean",
          "description": "Property. Model:'https://schema.org/Boolean'. Gives the ignition status of the vehicle. True means ignited"
        },
},
...// MORE CODE OMITTED FOR BREVITY
}
```
<p align="right"><a href="#top">☝</a></p>

### 💠minLength-maxLength

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"familyName": {
      "type": "string",
      "minLength": 1,
      "maxLength": 256
    }
... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠number

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"cargoWeight": {
          "type": "number",
          "description": "Property. Current weight of the vehicle's cargo. Model:'https://schema.org/Number'. Units:'Kilograms'",
          "minimum": 0,
          "exclusiveMinimum": true
        },
... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠minimum-maximum

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"height": {
      "type": "number",
      "format": "double",
      "minimum": 0.0,
      "maximum": 3.0
    }
... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠date

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"dateVehicleFirstRegistered": {
          "type": "string",
          "format": "date",
          "description": "Property. The date of the first registration of the vehicle with the respective public authorities. Model:'https://schema.org/dateVehicleFirstRegistered'"
        },
... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠date-time

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"purchaseDate": {
          "type": "string",
          "format": "date-time",
          "description": "Property. The date the item e.g. vehicle was purchased by the current owner. Model:'https://schema.org/purchaseDate'"
        },
... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠arrays

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"tags": {
      "description": "Tags for the blog",
      "type": "array",
      "items": {
         "type": "string"
       },
       "minItems": 1,   
       "uniqueItems": true
    }
... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠arrays-prefixItems

Tuple validation is useful when the array is a collection of items where each has a different schema and the ordinal index of each item is meaningful.

For example, you may represent a street address such as 1600 Pennsylvania Avenue NW as a 4-tuple of the form:

[number, street_name, street_type, direction]

Each of these fields will have a different schema:

- number: The address number. Must be a number.
- street_name: The name of the street. Must be a string.
- street_type: The type of street. Should be a string from a fixed set of values.
- direction: The city quadrant of the address. Should be a string from a different set of values.

The prefixItems keyword is an array, where each item is a schema that corresponds to each index of the document's array. That is, an array where the first element validates the first element of the input array, the second element validates the second element of the input array, etc.

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"street_address": {
      "description": "street address as a 4-tuple",
      "type": "array",
      "prefixItems": [
            { "type": "number" },
            { "type": "string" },
            { "enum": ["Street", "Avenue", "Boulevard"] },
            { "enum": ["NW", "NE", "SW", "SE"] }
        ]
    }
... // MORE CODE OMITTED FOR BREVITY
}

```

Example 

```json
[1600, "Pennsylvania", "Avenue", "NW"]
```
<p align="right"><a href="#top">☝</a></p>

### 💠defs

Sometimes we have small subschemas that are only intended for use in the current schema and it doesn't make sense to define them as separate schemas. The [$defs](https://json-schema.org/understanding-json-schema/structuring#defs) keyword gives us a standardized place to keep subschemas intended for reuse in the current schema document.

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"properties": {
        "primaryName": { "$ref": "#/$defs/personName" }
    },
... // MORE CODE OMITTED FOR BREVITY
"$defs": {
        "personName": {
            "type": "object",
            "properties": {
                "firstName": { "type": "string" },
                "lastName": { "type": "string" }
            },
            "additionalProperties": false
        }
}

```

Another usage

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
"properties": {
        "address": { "$ref": "#/$defs/address" }
    },
... // MORE CODE OMITTED FOR BREVITY
"$defs": {
        "address": {
            "type": "object",
            "properties": {
                "line1": { "type": "string" },
                "line2": { "type": "string" },
                "line3": { "type": "string" },
                "line4": { "type": "string" },
                "postalCode": { "type": "string" },
                "country": { "type": "string" }
            },
            "additionalProperties": false
        }
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠refs

The [$ref](https://json-schema.org/understanding-json-schema/structuring#recursion) keyword may be used to create recursive schemas that refer to themselves. For example, you might have a person schema that has an array of children, each of which are also person instances.

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
  "properties": {
    "name": { "type": "string" },
    "lastname": { "type": "string" },
    "children": {
      "type": "array",
      "items": { "$ref": "#" }
    }
  }
  ... // MORE CODE OMITTED FOR BREVITY
}

```

usage of recursive schema

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
  "name": "Elizabeth",
  "lastname": "Thomas",
  "children": [
    {
      "name": "Charles",
      "lastname": "Evans",
      "children": [
        {
          "name": "William",
          "lastname": "Davies",
          "children": [
            { 
                "name": "George",
                "lastname": "Taylor", 
            },
            { 
                "name": "Charlotte",
                "lastname": "Brown",
            }
          ]
        },
        {
          "name": "Harry",
          "lastname": "Smith",
        }
      ]
    }
  ]
  ... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠External refs

```json

{
  ... // MORE CODE OMITTED FOR BREVITY!!
  "properties": {
    "previousLocation": {
          "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons/properties/location"
        },
  }
  ... // MORE CODE OMITTED FOR BREVITY
}

```

external schema section

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
  "properties": {
    "location": {
          "oneOf": [
            {
              "title": "GeoJSON Point",
              "type": "object",
              "required": [
                "type",
                "coordinates"
              ],
              "description": "GeoProperty. Geojson reference to the item. Point"
              ...
  }
  ... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠arrays and defs combinations

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
 "properties": {
        "addressHistory": {
            "type": "array",
            "items": { "$ref": "#/$defs/address" }
        }
    },
    "additionalProperties": false,
    "$defs": {
        "address": {
            "type": "object",
            "properties": {
                "line1": { "type": "string" },
                "line2": { "type": "string" },
                "townOrCity": { "type": "string" },
                "region": { "type": "string" },
                "postalCode": { "type": "string" },
            },
            "additionalProperties": false
        }
    }
  ... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠defs with enums

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
 "properties": {
    "shipping_address": { "$ref": "/schemas/address" },
    "billing_address": { "$ref": "/schemas/address" }
     },
    "additionalProperties": false,
    "$defs": {
            "address": {
                "$id": "https://example.com/schemas/address",
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "properties": {
                    "street_address": { "type": "string" },
                    "city": { "type": "string" },
                    "state": { "$ref": "#/definitions/state" }
                },
                "required": ["street_address", "city", "state"],
                "definitions": {
                        "state": { "enum": ["CA", "NY", "... etc ..."] }
                }
            }
    }
  ... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠strings with enums

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
 "properties": {
        "type": {
                "type": "string",
                "description": "Property. Indicates whether the vehicle is been used for special purposes, like commercial rental, driving school, or as a taxi. The legislation in many countries requires this information to be revealed when offering a car for sale. Model:'https://schema.org/vehicleSpecialUsage'. Enum:'ambulance, fireBrigade, military, police, schoolTransportation, taxi, trashManagement'",
                "enum": [
                    "Bus", "Car", "Caravan", "Dumper", "E-Bike", "E-Moped", "E-Scooter", "E-Motorcycle", "FireTender",
                ]
            },
  ... // MORE CODE OMITTED FOR BREVITY
}

```

Another example

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
 "properties": {
        "deviceBatteryStatus": {
          "type": "string",
          "enum": [
            "connected",
            "disconnected"
          ],
          "description": "Property. Model:'https://schema.org/Text'. Gives the Battery charging status of the reporting device. Enum:'connected, disconnected'"
        },
 },
  ... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠array with enums

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
 "properties": {
        "category": {
            "type": "array",
            "description": "Property. Vehicle category(ies) from an external point of view. This is different than the vehicle type (car, lorry, etc.) represented by the `vehicleType` property. Model:'https://schema.org/Text'. Enum:'municipalServices, nonTracked, private, public, specialUsage, tracked'. Tracked vehicles are those vehicles which position is permanently tracked by a remote system. Or any other needed by an application They incorporate a GPS receiver together with a network connection to periodically update a reported position (location, speed, heading ...)",
            "items": {
                "type": "string",
                "enum": [
                "municipalServices",
                "nonTracked",
                "private",
                "public",
                "specialUsage",
                "tracked"
                ]
            }
        },
  ... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠Reusing common types

In the next example, we constrained all of our types to a string of length 1-256.

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
 "properties": {
        "familyName": {
            "type": "string",
            "minLength": 1,
            "maxLength": 256
        },
        "givenName": {
            "type": "string",
            "minLength": 1,
            "maxLength": 256
        },
        "otherNames": {
            "type": "string",
            "minLength": 1,
            "maxLength": 256
        },
  ... // MORE CODE OMITTED FOR BREVITY
}

```

We can simplify this by re-using a reference to a common schema with the $ref keyword.

```json

{
  ... // MORE CODE OMITTED FOR BREVITY
 "properties": {
        "properties": {
            "familyName": { "$ref": "#/$defs/constrainedString" },
            "givenName": { "$ref": "#/$defs/constrainedString" },
            "otherNames": { "$ref": "#/$defs/constrainedString" },
        },
 "$defs": {
    "constrainedString": {
      "type": "string",
      "minLength": 1,
      "maxLength": 256
    }
  }
  ... // MORE CODE OMITTED FOR BREVITY
}

```
<p align="right"><a href="#top">☝</a></p>

### 💠object type

```json
{
...// MORE CODE OMITTED FOR BREVITY
"properties": {
                "municipalityInfo": {
                "type": "object",
                "description": "Property. Model:'https://schema.org/Text. Municipality information corresponding to this observation",
                "properties": {
                    "district": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. District name corresponding to this observation"
                        },
                    "ulbName": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. Name of the Urban Local Body corresponding to this observation"
                        },
                    "cityId": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. City ID corresponding to this observation"
                        },
                    "wardId": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. Ward ID corresponding to this observation"
                        },
                    "stateName": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. Name of the state corresponding to this observation"
                        },
                    "cityName": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. City name corresponding to this observation"
                        },
                    "zoneName": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. Zone name corresponding to this observation"
                        },
                    "zoneId": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. Zone ID corresponding to this observation"
                        },
                    "wardName": {
                        "type": "string",
                        "description": "Property. Model:'https://schema.org/Text'. Ward name corresponding to this observation"
                        },
                    "wardNum": {
                        "type": "number",
                        "description": "Property. Model:'https://schema.org/Number'. Ward number corresponding to this observation"
                        }
                }
               }
},
...// MORE CODE OMITTED FOR BREVITY
}
```
<p align="right"><a href="#top">☝</a></p>

### 💠allOf

To validate against allOf, the given data must be valid against all of the given subschemas. The allOf keyword is used to specify that a given instance must validate against all of the subschemas provided within an array. It’s essentially a logical "AND" operation where all conditions must be met for validation to pass.

```json
{
...// MORE CODE OMITTED FOR BREVITY
"allOf": [
    { "type": "string" },
    { "maxLength": 5 }
  ]
...// MORE CODE OMITTED FOR BREVITY
}
```
<p align="right"><a href="#top">☝</a></p>

### 💠oneOf

To validate against oneOf, the given data must be valid against exactly one of the given subschemas.

```json
{
...// MORE CODE OMITTED FOR BREVITY
"properties": {
        "SINGLE_CHOICE": {
            "type": "string",
            "title": "Single choice",
            "description": "Some description",
            "oneOf": [
                    {
                    "const": "Yes",
                    "title": "Yes"
                    },
                    {
                    "const": "No",
                    "title": "No"
                    }
            ]
        },
},
...// MORE CODE OMITTED FOR BREVITY
}
```

Another example

```json
{
...// MORE CODE OMITTED FOR BREVITY
"oneOf": [
    { "type": "number", "multipleOf": 5 },
    { "type": "number", "multipleOf": 3 }
  ]
...// MORE CODE OMITTED FOR BREVITY
}
```
Another example

```json
{
...// MORE CODE OMITTED FOR BREVITY
"properties": {
        "speed": {
            "oneOf": [
                {
                "type": "number",
                "minimum": 0
                },
                {
                "type": "number",
                "minimum": 1,
                "maximum": 75
                }
            ],
            "description": "Property. Denotes the magnitude of the horizontal component of the vehicle's current velocity and is specified in Kilometers per Hour. If provided, the value of the speed attribute must be a non-negative real number. `-1` MAY be used if speed is transiently unknown for some reason. Model:'https://schema.org/Number'. Units:'Km/h'"
        },
},
...// MORE CODE OMITTED FOR BREVITY
}
```
<p align="right"><a href="#top">☝</a></p>

### 💠anyOf

To validate against anyOf, the given data must be valid against any (one or more) of the given subschemas.

```json
{
...// MORE CODE OMITTED FOR BREVITY
"anyOf": [
    { "type": "string", "maxLength": 5 },
    { "type": "number", "minimum": 0 }
  ]
...// MORE CODE OMITTED FOR BREVITY
}
```

Another example

```json
{
...// MORE CODE OMITTED FOR BREVITY
"properties": {
        "refVehicleModel": {
            "anyOf": [
                {
                "type": "string",
                "minLength": 1,
                "maxLength": 256,
                "pattern": "^[\\w\\-\\.\\{\\}\\$\\+\\*\\[\\]`|~^@!,:\\\\]+$",
                "description": "Property. Identifier format of any NGSI entity"
                },
                {
                "type": "string",
                "format": "uri",
                "description": "Property. Identifier format of any NGSI entity"
                }
            ],
            "description": "Relationship. Model:'https://schema.org/URL'. Reference to a VehicleModel"
        },
},
...// MORE CODE OMITTED FOR BREVITY
}
```
<p align="right"><a href="#top">☝</a></p>

### 💠Third-party solutions

- [Newtonsoft's paid-for extension to JSON.NET](https://www.newtonsoft.com/jsonschema)
- [Greg Dennis's Json-Everything](https://github.com/gregsdennis/json-everything)
- [Rico Suter's NJsonSchema](https://github.com/RicoSuter/NJsonSchema)

<p align="right"><a href="#top">☝</a></p>

## 📚Acknowledgments

- [JSON Schema](https://json-schema.org/docs)
- [array](https://json-schema.org/understanding-json-schema/reference/array)
- [Creating your first schema](https://json-schema.org/learn/getting-started-step-by-step#creating-your-first-schema)
- [Structuring a complex schema](https://json-schema.org/understanding-json-schema/structuring#structuring-a-complex-schema)
- [C# serialization with JsonSchema and System.Text.Json](https://endjin.com/blog/2021/05/csharp-serialization-with-system-text-json-schema)
- [Json Schema Patterns in .NET - Data Object](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-data-object)
- [Json Schema Patterns in .NET - Reusing Common Types](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-reusing-common-types)
- [Json Schema Patterns in .NET - Polymorphism with discriminator properties](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-polymorphism-with-discriminator-properties)
- [NJsonSchema](https://github.com/RicoSuter/NJsonSchema)
- [Generate JSON Schema validator from fluent code in .NET](https://medium.com/@lateapexearlyspeed/generate-json-schema-validator-from-fluent-code-in-net-8cbdbb933e27)
- [dataModel.Transportation](https://github.com/smart-data-models/dataModel.Transportation/blob/master/Vehicle/schema.json)
- [JSON Schema Docs](https://www.learnjsonschema.com/2020-12/)


### To review

- [Json Schema Patterns in .NET - Open vs. Closed Types](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-open-versus-closed-types)
- [Json Schema Patterns in .NET - Extending a base type](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-extending-base-type)
- [Json Schema Patterns in .NET - Constraining a base type](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-constraining-a-base-type)
- [Json Schema Patterns in .NET - Creating a strongly typed array](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-creating-strongly-typed-array)
- [Json Schema Patterns in .NET - Creating an array of higher rank](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-creating-array-of-higher-rank)
- [Json Schema Patterns in .NET - Working with tensors](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-working-with-tensors)
- [Json Schema Patterns in .NET - Creating tuples](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-creating-tuples)
- [Json Schema Patterns in .NET - Interfaces and mix-in types](https://endjin.com/blog/2024/05/json-schema-patterns-dotnet-interfaces-and-mix-in-types)