
# Load your Azure SQL database with data

[![databases/mssql/load-your-mssql-database-with-data/README.md](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/databases_mssql_load-your-mssql-database-with-data_README_md.yml/badge.svg)](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/databases_mssql_load-your-mssql-database-with-data_README_md.yml)

## Prerequisites

This example assumes you have previously completed the following examples:

1. [Create an Azure Resource Group](../../../general/group/create/README.md)
1. [Create an Azure SQL Database](../create/README.md)
1. [Install curl](https://curl.haxx.se/download.html)
1. [Open Azure SQL server firewall to your IP address](../open-firewall-to-your-ip/README.md)
1. [Install mssql-cli client](https://docs.microsoft.com/en-us/sql/tools/mssql-cli?view=sql-server-ver15)

<!-- workflow.cron(0 3 * * 5) -->
<!-- workflow.include(../open-firewall-to-your-ip/README.md) -->

## Load your Azure SQL database with data

To load the Azure SQL database with data execute the following command lines to
connect to the database:

<!-- workflow.skip() -->
```shell
  export MSSQL_DNS_NAME=`az sql server show \
    --resource-group $RESOURCE_GROUP \
    --name $MYSQL_NAME \
    --query fullyQualifiedDomainName \
    --output tsv`

  export MSSQL_CLIENT_USERNAME="$MSSQL_USERNAME@$MSSQL_NAME"

  mssql-cli -S $MSSQL_DNS_NAME -U $MSSQL_CLIENT_USERNAME -P $MSSQL_PASSWORD -i create.sql

  mssql-cli -S $MSSQL_DNS_NAME -U $MSSQL_CLIENT_USERNAME -P $MSSQL_PASSWORD -d demo -i load.sql
```

>
> If your country is missing from the SQL file please let us know by filing a
> GitHub issue or by issuing a PR against this repository.
>

<!-- workflow.run()

  cd databases/mssql/load-your-mssql-database-with-data

  sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 1
  python -m pip install --upgrade pip
  sudo pip install mssql-cli

  export MSSQL_DNS_NAME=`az sql server show \
    --resource-group $RESOURCE_GROUP \
    --name $MSSQL_NAME \
    --query fullyQualifiedDomainName \
    --output tsv`

  export MSSQL_CLIENT_USERNAME="$MSSQL_USERNAME@$MSSQL_NAME"

  mssql-cli -S $MSSQL_DNS_NAME -U $MSSQL_CLIENT_USERNAME -P $MSSQL_PASSWORD -i create.sql

  mssql-cli -S $MSSQL_DNS_NAME -U $MSSQL_CLIENT_USERNAME -P $MSSQL_PASSWORD -d demo -i load.sql

  cd ../../..

  -->

## Cleanup

Do NOT forget to remove the resources once you are done running the example.

<!-- workflow.directOnly()

  az group delete --name $RESOURCE_GROUP --yes || true

  -->

1m
