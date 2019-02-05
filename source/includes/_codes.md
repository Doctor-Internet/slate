# Response Codes

The Limelight API uses the following HTTP codes:

Code | Meaning | Used by
---------- | ------- | --- 
200 | Success. | GET, PUT, DELETE
201 | Resource Created. | POST
301 | Redirection. | *
400 | Bad Request. | *
401 | No authorization header sent. | *
403 | Bad / Invalid authorization. | *
404 | Invalid endpoint. | *
405 | Bad method. | *
500 | Internal Server Error | *
502 | Gateway Error | *
503 | Service Unavaliable | *