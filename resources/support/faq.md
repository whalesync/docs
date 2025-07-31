---
description: Frequently asked questions
---

# FAQ

## How is Whalesync different from Zapier?

In short, Zapier is an _automation_ tool whereas Whalesync is a _data syncing_ tool. Zapier is highly flexible and lets you architect logic such as “when a record is updated in Airtable, create a new record in Webflow, and then send an email.”&#x20;

Whalesync is less flexible BUT amazing at keeping two data sources in sync with little effort. You just connect Airtable and Webflow and Whalesync creates, updates, and deletes records bi-directionally automatically.

For a more detailed breakdown, check out: [How is Whalesync different from Zapier?](https://www.whalesync.com/blog/how-is-whalesync-different-from-zapier)

## How does Whalesync count records?

Whalesync only counts the records that you keep in sync and we don't "double-count" records across a Whalesync base.\
\
For example, let's say you have two Airtable bases:

* Base 1 → 100 records
* Base 2 → 0 records

Then you use Whalesync to sync Base 1 and Base 2, so now each has:

* Base 1 → 100 records (in sync)
* Base 2 → 100 records (in sync)

In total Whalesync would count that as 100 records.\
\
If you have other Airtable bases in your account (e.g. Base 3, Base 4, etc.). None of those would count towards your Whalesync total until you start syncing them.

## What data does Whalesync store?

While there are slight differences for each connector, as a general rule, Whalesync stores your:

* Records
* Database/site ID
* Table/column names and IDs
* API keys

Our database uses encryption for data storage. We encrypt API keys and private URLs at rest with [AES-256](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), thus double encryption for those.

As an example, for Airtable, Whalesync stores your records, your Airtable base ID, table name, column names, your Airtable API key, and a URL to a private view of your base.

## If I pause my subscription, will Whalesync keep my syncs?

Yes, if you pause your subscription, syncing will be disabled but Whalesync will not delete your sync configurations.

If you reactivate your subscription in the future, you will be able to resume your syncs and all pending changes will be synced over.
