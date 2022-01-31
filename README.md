# Restroom middleware for the Ledger Time Stamping Service

This library extends RESTroom and Zencode to allow them to user a Ledger TTS as data persistence layer.

Its goal is to allow developers for rapid prototyping of web services using cryptography, smart contracts, blockchain and DLT technologies.

## Usage


``` javascript
import express from "express";
import zencode from "@restroom-mw/core";
import ledger from "@restroom-mw/ledger-tts";

const app = express();

app.use(ledger);
app.use("/api/*", zencode);
```

## Zencode usage

The syntax of the actions is available here.

## Store data on the Ledger Timestamping Service

Use this Zencode:

```
# Here we are telling Zenroom where the Ledger service is and which Ledger endpoint call 
Given I have a ledger uri named 'uri'
Given that I have a ledger endpoint named 'endpoint'
Given that I have a method named 'method'

# Here we create an array ob objects
When I create the array of '8' random objects of '256' bits

# Here we print the output that we want to be stamped by the service
# If you don't print the output, restroom-mw won't save it in the database
Then print all data

# Here we are asking restroom-mw to store what has just been printed out, into the Ledger TTS
Then I save the 'array' into ledger
```

With this keys:

```
{
    "uri": "https://example.com",
    "endpoint": "stamp",
    "method": "POST"
}
```

## Get a stamp from the Ledger Timestamping Service

Use this Zencode:

```
# Here we are telling Zenroom which Ledger endpoint call 
Given I have a ledger uri named 'uri'
Given that I have a ledger endpoint named 'endpoint'
Given that I have a method named 'method'

# here we are telling Zenroom to 'allocate' a string dictionary, that 
# we'll use to store the data read from the database
Given I have a 'string dictionary' named 'myResult'

# Here we are reading the stamp with hash '2e016af539de750e1d6d396e383aa0b011c0e0e8b6861557679985894fac3eb2'
Given I read the record '2e016af539de750e1d6d396e383aa0b011c0e0e8b6861557679985894fac3eb2' save the result into 'myResult'

Then print 'myResult'
```

With this keys:

```
{
    "uri": "https://example.com",
    "endpoint": "stamp",
    "method": "GET"
    "hash": "2e016af539de750e1d6d396e383aa0b011c0e0e8b6861557679985894fac3eb2"
}
```


## Acknowledgements

LEDGER has received funding from the European Union’s Horizon 2020 research and innovation programme under the Grant Agreement no 825268.

## Links

https://ledgerproject.eu/
https://zenroom.org/
https://dyne.github.io/restroom-mw/#/

## License

This library is licensed under the GNU Affero General Public License v3.0