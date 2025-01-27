
# Deploy Jetty using a Docker image

[![compute/appservice/docker-jetty/README.md](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/compute_appservice_docker-jetty_README_md.yml/badge.svg)](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/compute_appservice_docker-jetty_README_md.yml)

## Prerequisites

This example assumes you have previously completed the following examples:

1. [Create an Azure Resource Group](../../../general/group/create/README.md)
1. [Create an Azure Container Registry](../../../containers/acr/create/README.md)
1. [Push a Jetty Docker image to Azure Container Registry](../../../containers/acr/jetty/README.md)
1. [Create settings.xml using admin access keys](../../../containers/acr/create-settings-xml/README.md)
1. [Create an Azure App Service Plan](../create-plan/README.md)

## Deploy Jetty using a Docker image

<!-- workflow.cron(0 8 * * 1) -->
<!-- workflow.include(../../../containers/acr/jetty/README.md) -->
<!-- workflow.include(../../../containers/acr/create-settings-xml/README.md) -->
<!-- workflow.include(../create-plan/README.md) -->

<!-- workflow.run() 

cd compute/appservice/docker-jetty

  -->

To deploy Jetty use the following command lines:

```shell
  export APPSERVICE_DOCKER_JETTY=appservice-docker-jetty-$RANDOM

  mvn azure-webapp:deploy \
    --settings=$SETTINGS_XML \
    -DappName=$APPSERVICE_DOCKER_JETTY \
    -DimageName=$ACR_JETTY_IMAGE \
    -DappServicePlan=$APPSERVICE_PLAN \
    -DresourceGroup=$RESOURCE_GROUP \
    -DserverId=$ACR_NAME

  az webapp show \
    --resource-group $RESOURCE_GROUP \
    --name $APPSERVICE_DOCKER_JETTY \
    --query 'hostNames[0]' \
    --output tsv
```

<!-- workflow.run()

sleep 180
cd ../../..

  -->

Then open your browser to the URL shown as output and you should see:

```text
And this is served by a custom Jetty using a Docker image coming from our 
own Azure Container Registry.
```

<!-- workflow.directOnly()

export RESULT=$(az webapp show --resource-group $RESOURCE_GROUP --name $APPSERVICE_DOCKER_JETTY --output tsv --query state)
if [[ "$RESULT" != Running ]]; then
  echo 'Web application is NOT running'
  az group delete --name $RESOURCE_GROUP --yes || true
  exit 1
fi

export URL=https://$(az webapp show --resource-group $RESOURCE_GROUP --name $APPSERVICE_DOCKER_JETTY --output tsv --query defaultHostName)
export RESULT=$(curl $URL)

az group delete --name $RESOURCE_GROUP --yes || true

if [[ "$RESULT" != *"custom Jetty"* ]]; then
  echo "Response did not contain 'custom Jetty'"
  exit 1
fi

  -->

## Properties supported by the example

The example supports the following properties that you can pass in as -Dname=value
to the Maven command line to customize your deployment.

| name                   | description                       |
|------------------------|-----------------------------------|
| `appName`              | the application name              |
| `appServicePlan`       | the App Service plan to use       |
| `imageName`            | the Docker image name             |
| `serverId`             | the Maven server id               |
| `registry`             | the Azure Container Registry name |
| `registryUrl`          | the Azure Container Registry url  |
| `resourceGroup`        | the Azure Resource Group name     |

## Cleanup

Do NOT forget to remove the resources once you are done running the example.

3m
