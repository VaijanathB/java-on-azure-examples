
# Load your MySQL database with data

[![databases/mysql/load-your-mysql-database-with-data/README.md](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/databases_mysql_load-your-mysql-database-with-data_README_md.yml/badge.svg)](https://github.com/Azure-Samples/java-on-azure-examples/actions/workflows/databases_mysql_load-your-mysql-database-with-data_README_md.yml)

## Prerequisites

This example assumes you have previously completed the following examples:

1. [Create an Azure Resource Group](../../../general/group/create/README.md)
1. [Create an Azure Database for MySQL](../create/README.md)
1. [Install curl](https://curl.haxx.se/download.html)
1. [Open MySQL server firewall to your IP address](../open-firewall-to-your-ip/README.md)
1. [Install mysql client](https://dev.mysql.com/downloads/README.md)

<!-- workflow.include(../open-firewall-to-your-ip/README.md) -->

## Load your MySQL database with data

To load the MySQL database with data execute the following command lines to
connect to the database:

<!-- workflow.skip() -->
```shell
  export MYSQL_DNS_NAME=`az mysql server show \
    --resource-group $RESOURCE_GROUP \
    --name $MYSQL_NAME \
    --query fullyQualifiedDomainName \
    --output tsv`

  export MYSQL_CLIENT_USERNAME="$MYSQL_USERNAME@$MYSQL_NAME"

  mysql -h $MYSQL_DNS_NAME -u $MYSQL_CLIENT_USERNAME -p$MYSQL_PASSWORD
```

Then use the following command line to load the `load.sql` file into the
database:

<!-- workflow.skip() -->
```shell
  source load.sql;
```

And to exit the `mysql` tool use the following command line:

<!-- workflow.skip() -->
```shell
  \q
```

>
> If your country is missing from the SQL file please let us know by filing a
> GitHub issue or by issuing a PR against this repository.
>


<!-- workflow.run()

  cd databases/mysql/load-your-mysql-database-with-data

  export MYSQL_DNS_NAME=`az mysql server show \
    --resource-group $RESOURCE_GROUP \
    --name $MYSQL_NAME \
    --query fullyQualifiedDomainName \
    --output tsv`

  export MYSQL_CLIENT_USERNAME="$MYSQL_USERNAME@$MYSQL_NAME"

  mysql -h $MYSQL_DNS_NAME -u $MYSQL_CLIENT_USERNAME -p$MYSQL_PASSWORD < load.sql

  cd ../../..

  -->

## Cleanup

Do NOT forget to remove the resources once you are done running the example.

<!-- workflow.directOnly()

  az group delete --name $RESOURCE_GROUP --yes || true

  -->

## Next steps

* [Azure Database for MySQL Documentation](https://docs.microsoft.com/en-us/azure/mysql/README.md)
* [Migrate to Azure Database for MySQL](https://datamigration.microsoft.com/scenario/mysql-to-azuremysql)
* [Minimal downtime migration](https://docs.microsoft.com/en-us/azure/mysql/howto-migrate-online)
* [Query data using Java](https://docs.microsoft.com/en-us/azure/mysql/connect-java)
* [Manage Azure Database for MySQL servers](https://docs.microsoft.com/en-us/cli/azure/mysql)

1m
