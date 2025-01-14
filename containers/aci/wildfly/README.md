
# Deploy WildFly

[![containers/aci/wildfly/README.md](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/containers_aci_wildfly_README_md.yml/badge.svg)](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/containers_aci_wildfly_README_md.yml)

## Prerequisites

This example assumes you have previously completed the following examples:

1. [Create an Azure Resource Group](../../../general/group/create/README.md)
1. [Create an Azure Container Registry](../../../containers/acr/create/README.md)
1. [Create an 'acrpull' Service Principal](../../../containers/acr/create-acrpull-service-principal/README.md)
1. [Push a WildFly Docker image to Azure Container Registry](../../../containers/acr/wildfly/README.md)

## Deploy WildFly

<!-- workflow.include(../../acr/create-acrpull-service-principal/README.md) -->
<!-- workflow.include(../../acr/wildfly/README.md) -->

To deploy WildFly use the following command line:

```shell
  export ACI_WILDFLY=aci-wildfly-$RANDOM

  az container create \
    --resource-group $RESOURCE_GROUP \
    --name $ACI_WILDFLY \
    --image $ACR_NAME.azurecr.io/$ACR_WILDFLY_IMAGE \
    --registry-login-server $ACR_NAME.azurecr.io \
    --registry-username $ACR_PULL_SERVICE_PRINCIPAL_ID \
    --registry-password $ACR_PULL_SERVICE_PRINCIPAL_PASSWORD \
    --dns-name-label $ACI_WILDFLY \
    --ports 8080

  echo `az container show \
    --resource-group $RESOURCE_GROUP \
    --name $ACI_WILDFLY \
    --query ipAddress.fqdn \
    --output tsv`:8080
```

<!-- workflow.run() 

  sleep 60

  -->

Then open your browser to the URL echoed above and you should see:

```text
And this is served by a custom WildFly using a Docker image coming from our 
own Azure Container Registry.
```

<!-- workflow.directOnly()

export URL=http://$(az container show --resource-group $RESOURCE_GROUP --name $ACI_WILDFLY --query ipAddress.fqdn --output tsv):8080
export RESULT=$(curl $URL)

az group delete --name $RESOURCE_GROUP --yes || true

if [[ "$RESULT" != *"custom WildFly"* ]]; then
  echo "Response did not contain 'custom WildFly'"
  exit 1
fi

  -->

## Cleanup

Do NOT forget to remove the resources once you are done running the example.

2m
