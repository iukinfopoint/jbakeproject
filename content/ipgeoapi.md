title=IP Geo API
date=2013-08-24
type= ipgeoapi
tags=blog
status=published
~~~~~~



# IP Geolocation API JQuery SDK

In this document, you will go through the basic steps to use IP Geolocation API JQuery SDK.  
You need a valid 'IPGeolocation API key' to use this SDK. [Sign up](https://ipgeolocation.io/signup) here and get your free API key if you don’t have one.

## System Requirements  

Internet connection is required to run this component.

## Installation
### CDN Link

Add the following script in your HTML page:

```html
<script src="https://cdn.jsdelivr.net/npm/ip-geolocation-api-jquery-sdk@1.0.6/ipgeolocation.min.js"></script>
```

## Geolocation Lookup

You can use this SDK without an API key if you're using the _Request Origin_ feaure on IP Geolocation API.  
Here are a few different ways of querying Geolocation for an IP address from IP Geolocation API.

```javascript
// Function to handle the response from IP Geolocation API.
// "response" is a JSON object returned from IP Geolocation API.
function handleResponse(response) {
    console.log(response);
}

// Get geolocation for the calling machine's IP address with an API key (optional, if you're using "Request Origin" feature at IP Geolocation API)
getGeolocation(handleResponse, "YOUR_API_KEY");

// Don't pass the API key if you're using the "Request Origin" feature at IP Geolocation API
getGeolocation(handleResponse);

// Toggle API calls' async behavior. By default, async is true.
setAsync(false)

// Get geolocation for an IP address "1.1.1.1"
setIPAddressParameter("1.1.1.1");
getGeolocation(handleResponse, "YOUR_API_KEY");

// Get geolocation for an IP address "1.1.1.1" in Russian language **
setLanguageParameter("ru");
setIPAddressParameter("1.1.1.1");
getGeolocation(handleResponse, "YOUR_API_KEY");

// Get the specific geolocation fields "country_code2,time_zone,currency" for the calling machine's IP address
setFieldsParameter("geo,time_zone,currency");
getGeolocation(handleResponse, "YOUR_API_KEY");

// Get the specified geolocaiton fields like "country_code2,time_zone,currency" for an IP address "1.1.1.1" and skip the "ip" field in the response
setFieldsParameter("geo,time_zone,currency");
setIPAddressParameter("1.1.1.1");
setExcludesParameter("ip");
getGeolocation(handleResponse, "YOUR_API_KEY");
```
## Time Zone API

Here are a few examples to query Time Zone information from Timezone API.

```javascript
// Function to handle the response from IP Geolocation API.
// "response" is a JSON object returned from IP Geolocation API.
function handleResponse(response) {
    console.log(response);
}

// Get time zone information for the calling machine's IP address with an API key (optional, if you're using "Request Origin" feature at IP Geolocation API)
getTimezone(handleResponse, "YOUR_API_KEY");

// Don't pass the API key if you're using the "Request Origin" feature at IP Geolocation API
getTimezone(handleResponse);

// Toggle API calls' async behavior. By default, async is true.
setAsync(false)

// Get time zone information for an IP address "1.1.1.1" and geolocation information in Italian language **
setIPAddressParameter("1.1.1.1");
setLanguageParameter("it");
getTimezone(handleResponse, "YOUR_API_KEY");

// Get time zone infomration for a time zone "America/New_York"
setTimezoneParameter("America/Los_Angeles");
getTimezone(handleResponse, "YOUR_API_KEY");

// Get time zone information by coordinates of the location
setCoordinatesParameter("31.4816", "74.3551");
getTimezone(handleResponse, "YOUR_API_KEY");
```

## Example

Here is a sample code to use IP Geolocation API using JQuery SDK:

```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/ip-geolocation-api-jquery-sdk@1.0.5/ipgeolocation.min.js"></script>

<script>
    var ip = sessionStorage.getItem("ip");
    var country_name = sessionStorage.getItem("country_name");
    var country_code2 = sessionStorage.getItem("country_code2");
            
    if (!ip || !country_name || !country_code2) {
        setAsync(false);
        setFieldsParameter("country_name,country_code2");
        getGeolocation(handleGeolocationResponse, "YOUR_API_KEY");
    }

    function handleGeolocationResponse(json) {
        ip = json.ip;
        country_name = json.country_name;
        country_code2 = json.country_code2;

        sessionStorage.setItem("ip", ip);
        sessionStorage.setItem("country_name", country_name);
        sessionStorage.setItem("country_code2", country_code2);
    }
                
    $(document).ready(function() {
        alert("Hello " + country_name + "!");
    });
</script>
```

** IPGeolocation provides geolocation information in the following languages:
* English (en)
* German (de)
* Russian (ru)
* Japanese (ja)
* French (fr)
* Chinese Simplified (cn)
* Spanish (es)
* Czech (cs)
* Italian (it)

By default, geolocation information is returned in English. Response in a language other than English is available to paid users only.

## Source Code

The complete source code for this SDK is avaliable at [Github](https://github.com/IPGeolocation/ip-geolocation-api-jQuery-sdk).
