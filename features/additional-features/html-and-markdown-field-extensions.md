---
description: >-
  Sync raw HTML and Markdown from Airtable, Google Sheets, and Postgres into a
  rich text field
---

# HTML and Markdown field extensions

### TLDR

Add "\_html" to a text field to sync HTML into a rich text field. Add "\_md" to a text field to sync Markdown to a rich text field.

### Details

Sometimes you want more control over your rich text and want to directly edit HTML, such as controlling the exact HTML that gets stored in a Webflow rich text field. For that, we built the HTML field extension feature.

If you add "\_html" to the end of a long text field in Airtable, Google Sheets, or Postgres, Whalesync will recognize that data as HTML. If you map that field to a rich text field in Webflow, we'll automatically convert your HTML into rich text.

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-17 at 4.19.35 PM.png" alt=""><figcaption></figcaption></figure>

![Rich text result in Webflow](<../../.gitbook/assets/html tag - rich text.png>)

### Markdown

In a Postgres or Supabase column, if you add "\_md" to the end of the column name, Whalesync will parse the data as Markdown and convert it to HTML. The column will be read-only on the Postgres/Supabase side, to prevent overwriting your Markdown with HTML. If you need two-way sync, use HTML instead.

In an Airtable field, if you add "\_md" to the end of a rich text field's name, Whalesync will **preserve** the Markdown in the data instead of converting to HTML. This is because Airtable's rich text fields store Markdown internally, and you can enter limited Markdown into an Airtable cell to format text.

{% hint style="warning" %}
Google Sheets does not currently support the Markdown field extension.
{% endhint %}

### **Things to keep in mind**

You will need to refresh your fields in Whalesync if you want to convert an existing field into an HTML or Markdown field.

{% embed url="https://www.loom.com/share/79d8cb821f3e43ec8edfd79e4ffa5da4?sid=e534524a-fd44-4246-bfa7-25ac5f77995e" %}

{% hint style="warning" %}
**If using an Airtable field as HTML, make sure "enable rich text formatting" is toggled off.**
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2023-04-26 at 17.30.25.png" alt=""><figcaption></figcaption></figure>

Make sure only the source side has the `_html` or `_md` extension on the field or column name. If the destination side has the suffix as well, Whalesync will sync the text form of the raw HTML or Markdown, escaped to display on your website or rich text field.
