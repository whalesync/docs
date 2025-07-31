---
cover: ../../.gitbook/assets/gitbook-cover_stripe.jpg
coverY: 0
---

# Stripe

## Stripe Connector Guide

This guide provides an overview of how to connect Whalesync to Stripe and answers common questions.

### Connecting to Stripe

To connect to Stripe, you'll need to [create your Stripe "Secret Key"](https://docs.whalesync.com/connectors/stripe/authorize-stripe). This key is a password that allows Whalesync to securely access your Stripe data.

You can find your Secret Key in your Stripe Dashboard under Developers > API keys. It is important that you copy the **Secret key** (it starts with `sk_...`), not the Publishable key (which starts with `pk_...`). Using a Publishable key will result in an error when you try to connect.

Common connection issues include:

* **Invalid Key**: If you get an error about an invalid key, check that you have copied the full Secret Key correctly.
* **Publishable Key Used**: If you see an authorization error, ensure you are using a Secret Key (`sk_...`) and not a Publishable key (`pk_...`).

For detailed instructions with screenshots, see our guide on [authorizing Stripe](https://docs.whalesync.com/connectors/stripe/authorize-stripe).

### Syncing Data

Whalesync can read data from many different objects in Stripe. Once you've connected your Stripe account, you can choose which of these to sync.

#### Supported Objects

| Tables            | Status               |
| ----------------- | -------------------- |
| 💵 Charges        | ➡️ Supported (1-Way) |
| 💵 Coupons        | ➡️ Supported (1-Way) |
| 👤 Customers      | ➡️ Supported (1-Way) |
| 📃 Invoice Items  | ➡️ Supported (1-Way) |
| 💵 Invoices       | ➡️ Supported (1-Way) |
| 🔗 Payment Links  | ➡️ Supported (1-Way) |
| 📃 Plans          | ➡️ Supported (1-Way) |
| 💵 Prices         | ➡️ Supported (1-Way) |
| 📦 Products       | ➡️ Supported (1-Way) |
| 📣Promotion Codes | ➡️ Supported (1-Way) |
| 💵 Refunds        | ➡️ Supported (1-Way) |
| 📃 Subscription   | ➡️ Supported (1-Way) |

### Things to Keep in Mind

* **Read-Only Sync**: Stripe is a "read-only" connector. This means Whalesync can pull data _from_ Stripe into other apps, but cannot push data _to_ Stripe. You will not be able to use Whalesync to create or update records in Stripe.
* **Data Formatting**: Some Stripe fields are converted to a more usable format in your destination app:
  * **Amounts**: Stripe stores money values in the smallest currency unit (e.g., cents). For example, a charge of $10.00 is stored as `1000` in Stripe. Whalesync automatically converts this to `10` so it displays as the correct dollar amount in other tools.
  * **Complex Fields**: Some fields in Stripe contain complex data, like a list of items or nested information. Whalesync converts these fields into a text format (JSON) so you can still access the data.

### Synthetic Fields

Whalesync adds a few fields to your data that are not originally from Stripe. These fields help Whalesync manage the sync and provide useful metadata. They are not writable.

| Name                      | Explanation                                                                                              | Writable |
| ------------------------- | -------------------------------------------------------------------------------------------------------- | -------- |
| Stripe Record ID          | A unique ID that Whalesync uses to keep track of records in Stripe. This is based on the ID from Stripe. | No       |
| Last Modified (Whalesync) | The timestamp of when Whalesync last updated the record in the destination app.                          | No       |

The table below lists all the Stripe objects (which Whalesync treats as tables) that you can sync.

### Supported Fields

Whalesync supports a variety of field types from Stripe. Here's a guide to what they mean:

* **String**: Plain text.
* **Integer**: Numbers without decimals.
* **Boolean**: A true/false value.
* **Timestamp**: Date and time information.
* **Currency**: A three-letter code for the currency (e.g., "USD").
* **Money**: A numerical value representing an amount of money.
* **Foreign Key**: A reference to another record. For example, a Charge record might have a Customer ID that links to a Customer record.
* **Expandable**: A special Stripe field that links to another Stripe object (like a Customer or Invoice). Whalesync automatically includes the full details of that linked object, shown as a block of text (JSON).
* **Hash / Array**: Fields that hold structured data, like a list of items. Whalesync converts these into readable text (JSON).
* **Enum**: A field that has a specific list of possible values, like the status of a payment.
