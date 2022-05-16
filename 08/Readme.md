# Create a multi-tier solution by using Azure services

Diagram

![](../media/Lab08-Diagram.png)


## Create an Azure App Service resource by using a Docker container image (httpbin container image)

- resoruce group name : ApiService
- name : httpapikie
- publish : Docker Container
- OS : Linux
- ASP : create new
  - name : ApiPlan
- SKU : S1
- Docker : 
  - Option : Single Container
  - Image Source : Docker Hub
  - Access Type : Public
  - Image : kennethreitz/httpbin:latest

## Test the httpbin web application

goto https://httpapikie.azurewebsites.net/

within the webapp select  ```Response formats``` > html > try it out > execute ```review Response body and Header```

![](../media/Lab08-1.png)

within the webapp , select ```Dynamic data``` > GET /byte/{n} > enter 25 > execute ```review Response body and Header```

![](../media/Lab08-2.png)


within the webapp , select ```Status codes``` > GET /status/{codes} > code : enter 404 > execute ```review Server Response```

![](../media/Lab08-3.png)

## Build an API proxy tier by using Azure API Management

Create APIM
- name : proapikie
- Org name : Contoso
- Admin email : admin@contoso.com
- Pricing tier : Consumption (99.95% SLA)


![](../media/Lab08-4.png)

## Define a new API

on the APIs Create a blank API
- Display name : HTTPBin API
- Name : httpbin-api
- Web service URL : https://httpapikie.azurewebsites.net/

![](../media/Lab08-5.png)

on the ```Design``` tab, select ```+ Add operation```

- Display name : Echo Headers
- Name : echo-headers
- Url : GET
- URL : /

![](../media/Lab08-6.png)

```Inbound Add policy (Inbound processing)```
- Name : source
- Value : Add Value , azure-api-mgmt
- Action : append

![](../media/Lab08-7.png)

```Backend``` select the pencil icon.

- Service URL section : Override
- Service URL text box : 
  - https://httpapikie.azurewebsites.net > change to > https://httpapikie.azurewebsites.net/headers


## Test API and Review Overwide Header


![](../media/Lab08-8.png)

![](../media/Lab08-9.png)


## Manipulate an API response

in the Design tab, select ```+ Add operation```.

- Display name : Get Legacy Data
- Name : get-legacy-data
- URL : GET
- URL : /xml

and then test https://proapikie.azure-api.net/xml

![](../media/Lab08-10.png)


Add policy > Outbound processing > select the ```Other policies``` tile

Replace that block of XML with the following XML

outbound XML to JSON

```xml
<outbound>
    <base />
    <xml-to-json kind="direct" apply="always" consider-accept-header="false" />
</outbound>
```

![](../media/Lab08-11.png)

Review the results of the API request

https://proapikie.azure-api.net/xml

![](../media/Lab08-12.png)

On the Design tab, select + Add operation

- Display name : Generate Payload
- Name :  generate-payload
- URL list : GET
- URL text box	: /bytes/{n}.
Template parameters section	In the TYPE text box, enter int.

![](../media/Lab08-13.png)

Outbound processing tile, select + Add policy > Validate content
limit size payload

- Unspecified content type action : 
- Maximum payload size (in bytes) : 128
- Size exceeded action : Prevent
- Errors variable name : validationErrors

![](../media/Lab08-14.png)

!! APIM BUG?? cannot limit all size

### Manipulate an API request

Add operation section

- Display name : Modify Status Code
- Name text box : modify-status-code
- URL list : GET
- URL text box : /status/404



In the Add inbound policy section, select the ```Rewrite URL```

![](../media/Lab08-15.png)

test before rewrite

![](../media/Lab08-16.png)


Rewriting 

![](../media/Lab08-17.png)


test after rewrited

![](../media/Lab08-18.png)


## Clean lab

```ps
az group delete --name ApiService --no-wait --yes
```






