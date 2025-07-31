# Authorize Postgres

Whalesync uses a [Postgres connection URI](https://www.postgresql.org/docs/current/libpq-connect.html#id-1.7.3.8.3.6) to connect to a database instance. The following pages describe how to find your connection URI from popular hosting services. If you don't see your hosting service, explore some of the other examples. Your hosting service should be something similar.

Depending on your settings, the connection string may need additional query parameters. You can add query parameters to the end of the URI by adding a question mark ("`?`"), followed by an option name, the equals sign, and a value. Additional parameters then are separated by an ampersand ("`&`"), followed by an option name, the equals sign, and a value. For example:

```
postgresql://postgres@hostname:5432/postgres?sslmode=require&client_encoding=auto
```

Depending on the service, you may need to experiment with different query parameters (especially those with SSL).

When encountering SSL or certificate issues, the "sslmode=no-verify" URL query parameter usually does the trick:

```
postgresql://postgres@hostname:5432/postgres?sslmode=no-verify
```

Please refer to your hosting service's documentation for the recommended settings. For more information regarding the possible query parameters you may need, please refer to these resources:

* [https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING](https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING)
* [https://github.com/brianc/node-postgres/tree/master/packages/pg-connection-string#tcp-connections](https://github.com/brianc/node-postgres/tree/master/packages/pg-connection-string#tcp-connections)

Note that Whalesync does not yet support:

* Whitelisted IP addresses
* Custom SSL/TLS certificates

If you need these to connect to your instance, please [reach out and let us know](../../../resources/support/).
