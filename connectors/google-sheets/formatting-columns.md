---
description: Quick guide on how to format columns (i.e. data types) in Google Sheets
---

# Formatting columns

### About data types

Google Sheets has two data type categories: 1) Numbers and 2) Text

<figure><img src="../../.gitbook/assets/Data Types.png" alt="" width="486"><figcaption></figcaption></figure>

### How to Format columns

To format a column in Google Sheets simply:

1. Highlight the column
2. Select "Format"
3. Choose the data type

<figure><img src="../../.gitbook/assets/Formatting a column.gif" alt=""><figcaption><p>Example formatting a column to the Date data type</p></figcaption></figure>

### Why formatting columns is important

In order to two-way sync fields, data types must match across your apps.

For example, if you have a `Date` field in Airtable and want to two-way sync it with Google Sheets, you'll need a `Date` field in Google Sheets.



### Data types in Google Sheets

#### Text

Text fields will two-way sync by default. No additional formatting is needed for:

* Text
* Long-text
* Drop-down
* Multiple Select
* Email

#### Numbers

Number fields need to be formatted in order to two-way sync:

1. Numbers
2. Percentages
3. Dates

#### Bonus: foreign keys

Learn how to use foreign keys in Google Sheets here:&#x20;

{% content-ref url="foreign-keys.md" %}
[foreign-keys.md](foreign-keys.md)
{% endcontent-ref %}

