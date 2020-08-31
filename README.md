# Red Hat Integration Demo

Red Hat Integration Demo

Topics include:
* 3Scale API Managment
* Fuse and Fuse Online
* Contract-first API Design and Testing

## Prerequisites

* Pre-create 3Scale namespace with pull secret and object storage secret.
* Pre-create Fuse Online namespace with pull secret.
* Pre-install API Designer
* Pre-install Microcks

## Demo Agenda

### Install / Upgrade Experience

1. [Brief intro to Red Hat Integration and OpenShift Container Platform](https://docs.google.com/presentation/d/1lI6fmYBrzrvs1zGoiP5rwHpQYPOGm85QizXqngSKF5g/edit#slide=id.g960315f43a_0_348)
2. Install 3Scale API Management using the 3Scale Operator.
3. Install Fuse Online using the Fuse Online operator.

### Explore 3Scale API Management

1. Explore Master tenant and create a new "demo" tenant.
2. Login to the demo tenant and explore "Echo API".
3. Import an [existing API](https://petstore.swagger.io/) using 3Scale Toolbox.
    * Import process
    * ActiveDocs
    * Metrics
    * Policies
4. Explore Admin interface and analytics.
5. Explore Developer Portal capabilities.

### Create a SOAP-to-REST Integration (Fuse Online)

1. Deploy a simple [SOAP Web Service](https://github.com/pittar/countries-soap-ws).
2. Login to Fuse Online.
    * Create a connection to the SOAP Web Service.
    * Create an integration by creating a new REST intefrace as a facade to the SOAP web service.
    * Deploy the integration and explore the Fuse Online dashboard.
    
### Create a SOAP-to-REST Integration (Fuse)

1. In CodeReady Studio, create a new **Fuse Integration**.
2. Delete the sample integration.
3. Create a new *Camel REST DSL from WSDL*
4. Explore the generated files and integration

### Contract First API Design and Testing (Apicurio and Microcks)

1. Create a new *OpenAPI 3* spec with Apicurio.
2. Define data types and methods.
3. Save the new OpenAPI Spec and import it into Microcks.
4. Save the Fuse code bundle.
5. Demo the mocked API with Postman.
6. Import API spec into 3Scale.
    
## Appendix

### Importing sample OpenAPI Spec.

1. First, add a new remote to the `3scale` cli:

```
$ 3scale remote add demo https://<token>@<tenant-admin url>
```

2. Next, import the API from the OpenAPI spec url:

```
$ 3scale import openapi -d demo --default-credentials-userkey user_key --target_system_name ps2 https://petstore.swagger.io/v2/swagger.json
```

3. Create a new `Application` Plan for the new API Product.

4. Under "Configuration -> Settings", change the auth key name to `api_key` to match the OpenAPI spec.

5. Change the "Credentials Location" to `As HTTP Headers`.

6. Add a `CORS` policy to the API after `3Scale APIcast`, and make sure the origins are set to `*`.

7. Save and promote the configuration through staging and production.

8. Make sure your default `Developer` account has registered a new `Application` for this API.  Copy the api key, as you'll need it in the Active Docs.

