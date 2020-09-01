# Using the 3Scale Toolbox CLI

## Import an API based on OpenAPI Spec

Although using the 3Scale Admin console is easy enough when it comes to adding new APIs to 3Scale, using the CLI can be faster and much more consistent, 
especially if your API already has an OpenAPI spec to start with.

For this example, we will import an existing demo API, the [Swagger Petstore API](https://petstore.swagger.io/).

## Prerequisites

* Install the [3Scale Toolbox CLI](https://github.com/3scale/3scale_toolbox_packaging/releases) locally, or use the provided [container image](https://access.redhat.com/documentation/en-us/red_hat_3scale_api_management/2.8/html/operating_3scale/the-threescale-toolbox#installing-the-toolbox).

## Import an API with 3Scale Toolbox CLI

1. From the command line, add a new "remote" for your 3Scale admin portal.
```
$ 3scale remote add <remote name> https://<admin token>@<admin portal url>
```
For this demo, we will assume the `<remote name` is "demo".

2. Import the OpenAPI spec from the spec URL.
```
$ 3scale import openapi -d demo --target_system_name petstore_demo https://petstore.swagger.io/v2/swagger.json
```

3. Create a new Application Plan for this service.
```
$ 3scale application-plan apply demo petstore_demo petstore_basic -n "Basic Plan" --default
```
