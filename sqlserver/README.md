# Microsoft SQL Server Check

# Overview

This check lets you track the performance of your SQL Server instances. It collects metrics for number of user connections, rate of SQL compilations, and more.

You can also create your own metrics by having the check run custom queries.

# Installation

The SQL Server check is packaged with the Agent, so simply [install the Agent](https://app.datadoghq.com/account/settings#agent) on your SQL Server instances. If you need the newest version of the check, install the `dd-check-sqlserver` package.

# Configuration

Create a file `sqlserver.yaml` in the Agent's `conf.d` directory:

```
init_config:

instances:
  - host: <SQL_HOST>,<SQL_PORT>
    username: <SQL_ADMIN_USER>
    password: <SQL_ADMIN_PASSWORD>
    connector: odbc # alternative is 'adodbapi'
    driver: SQL Server
```

See the [example check configuration](https://github.com/DataDog/integrations-core/blob/master/sqlserver/conf.yaml.example) for a comprehensive description of all options, including how to use custom queries to create your own metrics.

Restart the Agent to start sending SQL Server metrics to Datadog.

# Validation

Run the Agent's `info` subcommand and look for `sqlserver` under the Checks section:

```
  Checks
  ======
    [...]

    sqlserver
    -------
      - instance #0 [OK]
      - Collected 26 metrics, 0 events & 1 service check

    [...]
```

# Compatibility

The sqlserver check is compatible with all Windows and Linux platforms.

# Metrics

See [metadata.csv](https://github.com/DataDog/integrations-core/blob/master/sqlserver/metadata.csv) for a list of metrics provided by this check.

Most of these metrics come from your SQL Server's `sys.dm_os_performance_counters` table.

# Service Checks

**sqlserver.can_connect**:

Returns CRITICAL if the Agent cannot connect to SQL Server to collect metrics, otherwise OK.
