# txt2json.py
Convert human-readable text to valid JSON

usage: 
+ internal test data to stdout - txt2json.py
+ file to stdout - txt2json.py input-filename
+ file to file - txt2json.py input-filename output-filename

The input is delimited by whitespace and block tokens:
+ "" - quoted strings of any length
+ {} - JSON object
+ [] - JSON array
+ /* */ - comment of any length can contain any character

Strings which contain whitespace, or could be interpreted as numbers or as boolean, must be quoted

The file is assumed to be a JSON object, and the order of elements is preserved in the output JSON

Example input:
```
/* this is a 
comment */

key1 value1
key2 { has an object value }
key3 { x 2 y "3" }
key4 [ array value with 1 number ]

object {
    field1 { enum [ true false ] }
    field2 {
        colorcode [ 
            { blue 0 }
            { red 1 }
            { green 2 }
        ]
    }
}
```

The resulting JSON:

```
{
  "key1": "value1", 
  "key2": {
    "has": "an", 
    "object": "value"
  }, 
  "key3": {
    "x": 2, 
    "y": "3"
  }, 
  "key4": [
    "array", 
    "value", 
    "with", 
    1, 
    "number"
  ], 
  "object": {
    "field1": {
      "enum": [
        true, 
        false
      ]
    }, 
    "field2": {
      "colorcode": [
        {
          "blue": 0
        }, 
        {
          "red": 1
        }, 
        {
          "green": 2
        }
      ]
    }
  }
}
```