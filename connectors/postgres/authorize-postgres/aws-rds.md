---
description: >-
  How to find get your Postgres connection URI when using Amazon Web Services
  RDS
---

# AWS (RDS)

## Step 1: Find your database

Navigate to the AWS RDS dashboard. In the left panel you should see "Databases":

<figure><img src="../../../.gitbook/assets/image (26).png" alt="Screenshot of the AWS RDS side panel"><figcaption><p>Databases page</p></figcaption></figure>

In this list, select your database:

<figure><img src="../../../.gitbook/assets/image (31).png" alt="Screenshot of the AWS RDS database list"><figcaption><p>Database list in RDS</p></figcaption></figure>

## Step 2: Construct the connection URI

On the main database page, you should have the "Connectivity & security" tab selected. Note the endpoint and port number:

<figure><img src="../../../.gitbook/assets/image (24).png" alt="Screenshot of the AWS RDS endpoint and port information"><figcaption><p>RDS endpoint and port number</p></figcaption></figure>

Next under the "Configuration" tab, look up the username. You can also create a different user for Whalesync to connect, but for simplicity we'll use the master username:

<figure><img src="../../../.gitbook/assets/image (14).png" alt="Screenshot of AWS RDS database configuration"><figcaption><p>RDS configuration with the username</p></figcaption></figure>

The password was set when the database was originally created. Please ask whoever set up the database for the connection password.

Finally, construct the connection URI like this and replace `YOUR_PASSWORD` with the password:

{% code overflow="wrap" %}
```
postgresql://postgres:YOUR_PASSWORD@postgres-connector-test.000000000000.us-east-1.rds.amazonaws.com:5432/postgres
```
{% endcode %}

This is the string you will paste into the Whalesync Postgres connection dialog:

<figure><img src="../../../.gitbook/assets/image (28).png" alt="Screenshot of the Whalesync Postgres connection dialog"><figcaption><p>Enter your Postgres connection URI into Whalesync</p></figcaption></figure>

## Caveats

Note that Whalesync does not yet support:

* Whitelisted IP addresses
* Custom SSL/TLS certificates

If you need these to connect to your instance, please [reach out and let us know](../../../resources/support/).
