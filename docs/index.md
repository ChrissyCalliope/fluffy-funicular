# Configure Autoplay Countdown

Unlike the other topics, this contains two different pieces of documentation:
1. The *API Reference section* should be present in the Interfaces Guide. It points the reader to the Swagger file itself. 
1. The *Example: Autoplay Countdown* is a snippet showing the annotations that I would add to the Swagger file (API contract). I've shown some descriptions that I would add to a Swagger file.

## API Reference 

The REST API for this component is described following the open API Specification (or Swagger Specification). You can find the Open API file that describes your entire API (endpoints, parameters, authentication methods and document metadata), at the location:

https://&lt;host&gt;:&lt;port&gt;/Service/ 

Where &lt;host&gt; and &lt;port&gt; need to be replaced with your system's deployment location.

**Note:** You can use the **Try it Out** button for each of the endpoints, but be aware that you are actually hitting the endpoint at this location. Do not make any changes that you are not confident about.

## Example: Autoplay Countdown

The following is the input Open API / Swagger file (yaml) and some documentation. Note that this content (the values of the `description:` fields) is displayed at the preceding location, and will be transformed into a Swagger page that looks something like:  [http://petstore.swagger.io/](http://petstore.swagger.io/). 

```
---
  swagger: "2.0"
  info: 
    version: "1.0.0"
    title: "Swagger Autoplay API"
    description: >
      This documentation describes the endpoints that are associated with the Autoplay functionality. 
      Autoplay starts the next video on your Up Next list automatically, after a countdown is complete.
      Autoplay is enabled by default when viewed in a standard browser on a PC or handheld device. 
      Autoplay can be turned off manually by the user. 
      Autoplay will time out if the mobile device has been inactive on the network for 30 minutes, 
      Autoplay will time out if the Wifi has been inactive for 4 hours. 
  host: "autoplay.swagger.io"
  basePath: "/api"
  schemes: 
    - "http"
  consumes: 
    - "application/json"
  produces: 
    - "application/json"
  paths: 
    /autoplay/{countdown}: 
     post:
      description: > 
        This endpoint sets the countdown period for autoplay in seconds.
        This is the time window between the last video ending and the next one starting. 
        This value is only used if autoplay is enabled on the given device. 
      operationId: autoplayCountdown
      parameters:
        - name: countdown
          in: path
          description: > 
            Time period, in seconds, for the countdown between one video ending and the next one starting. 
            We recommend a countdown of 10 seconds, but suggest that you should set a maximum delay of 30 seconds. 
            0 indicates that there should be no countdown between the two videos. 
          required: true
          type: integer
          format: int64
      responses:
       ...
```

## Additional Items and Comments

* We could set a range for this value, capping the countdown period at, say, 30 seconds. That would seem a good design, but would be for the contract owner (BA?) to decide. 
* Document Type: Interfaces Guide
* It is likely that there would also need to be authentication and other high-level accompanying documentation.  
* This content re-uses the description of what auto-play actually is from the User Materials. 
* Reader: Developer, Service Operator
