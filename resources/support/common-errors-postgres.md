# Common errors - Postgres

### SSL errors while authorizing Postgres (e.g. "self-signed certificate in certificate chain")

When encountering SSL or certificate issues, the "sslmode=no-verify" URL query parameter at the end of your connection string usually does the trick:

```
postgresql://postgres@hostname:5432/postgres?sslmode=no-verify
```

Please see [authorize-postgres](../../connectors/postgres/authorize-postgres/ "mention") for more details about connection strings and URL query parameters.
