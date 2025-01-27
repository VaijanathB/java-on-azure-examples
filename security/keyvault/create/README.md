
# Create an Azure Key Vault

[![security/keyvault/create/README.md](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/security_keyvault_create_README_md.yml/badge.svg)](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/security_keyvault_create_README_md.yml)

## Prerequisites

This example assumes you have previously completed the following example:

1. [Create an Azure Resource Group](../../../general/group/create/README.md)

<!-- workflow.cron(58 12 * * 4) -->
<!-- workflow.include(../../../general/group/create/README.md) -->

## Create the Azure Key Vault

To create the Azure Key Vault use the following command lines:

```shell
  export KEYVAULT_NAME=keyvault-$RANDOM

  az keyvault create \
    --resource-group $RESOURCE_GROUP \
    --name $KEYVAULT_NAME
```

## Cleanup

Do NOT forget to remove the resources once you are done running the example.

<!-- workflow.directOnly()

export RESULT=$(az keyvault show --resource-group $RESOURCE_GROUP --name $KEYVAULT_NAME --output tsv --query properties.provisioningState)
if [[ "$RESULT" != Succeeded ]]; then
  echo 'Key vault was not provisioned'
  az group delete --name $RESOURCE_GROUP --yes || true
  exit 1
fi

az group delete --name $RESOURCE_GROUP --yes || true

  -->

## More information

1. [Azure CLI](https://docs.microsoft.com/cli/azure/keyvault)
1. [Azure Key Vault - documentation](https://docs.microsoft.com/azure/key-vault/README.md)
