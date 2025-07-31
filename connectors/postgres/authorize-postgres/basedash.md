---
description: How to find get your Postgres connection URI when using Basedash
---

# Basedash

<figure><img src="../../../.gitbook/assets/basedash_background (1).png" alt=""><figcaption></figcaption></figure>

## Step 1: Find your database

Navigate to the [Basedash Connections page](https://app.basedash.com/connections). In the left panel, scroll down to the bottom to see your databases. Click on the gear icon of the database you want to connect:

<div align="center"><figure><img src="../../../.gitbook/assets/image (19).png" alt="Screenshot of the settings icon for a database connection in Basedash"><figcaption><p>Connection settings for a database</p></figcaption></figure></div>

Click "Manage credentials":

<figure><img src="../../../.gitbook/assets/image (17).png" alt="Screenshot of the manage credentials button in Basedash"><figcaption><p>Manage credentials for a database</p></figcaption></figure>

## Step 2: Construct the connection URI

On the "Manage credentials" page, you should see a "SQL connection overview" section:

<figure><img src="../../../.gitbook/assets/image (8).png" alt="SQL connection overview page in Basedash"><figcaption><p>SQL connection overview</p></figcaption></figure>

Construct the connection URI with the above fields and replace `YOUR_PASSWORD` with the correct password. Using the example values above, the connection URI would look like this:

{% code overflow="wrap" %}
```
postgresql://postgres:YOUR_PASSWORD@18.18.98.1:5432/postgres
```
{% endcode %}

This is the string you will paste into the Whalesync Postgres connection dialog:

<figure><img src="../../../.gitbook/assets/image (16).png" alt="Screenshot of the Whalesync Postgres connection dialog"><figcaption><p>Enter your Postgres connection URI into Whalesync</p></figcaption></figure>

## Caveats

Note that Whalesync does not yet support:

* Whitelisted IP addresses
* Custom SSL/TLS certificates

If you need these to connect to your instance, please [reach out and let us know](../../../resources/support/).
