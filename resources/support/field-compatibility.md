---
description: Understanding why certain fields are not compatible and cannot be synced
---

# Field compatibility

### Why fields must be compatible

When syncing, you must map "compatible fields" so that Whalesync can translate data between your apps. In this translation, Whalesync handles much of the heavy lifting (like converting HTML to Markdown), but ultimately the data in these fields needs to work with each other.

### Relation fields and compatibility

<figure><img src="../../.gitbook/assets/Incompatible fields.png" alt=""><figcaption><p>Trying to map a relation field and only seeing incompatible options</p></figcaption></figure>

**Understanding reference fields**

One of the more advanced field types to map are ["relation fields"](../../features/additional-features/reference-fields.md) (aka "reference fields", "linked records", or "foreign keys"). These are fields that have a relation to another table.

Relation fields must be mapped to other relation fields in order to sync.

**How to find fields that are compatible with reference fields**

* If you're unsure how to create relation fields in your apps, check [our docs on relation fields](../../features/additional-features/reference-fields.md).
* In general, look for the squiggly arrow icon indicating a relation field (see screenshot above).



### Table of compatible fields

<table><thead><tr><th width="219.85546875">Field type (from: left, , to: top)</th><th>Normal text<select><option value="5YS9L34xs4mc" label="❌ Incompatible" color="blue"></option><option value="HpRBofSXFHA5" label="✅ Compatible" color="blue"></option></select></th><th>Rich text<select><option value="PFS2BxilCrgi" label="❌ Incompatible" color="blue"></option><option value="78DyTnPIRts4" label="✅ Compatible" color="blue"></option></select></th><th>URL<select><option value="I1FgKECS1Ci0" label="❌ Incompatible" color="blue"></option><option value="ppC0hWnlSnlO" label="✅ Compatible" color="blue"></option></select></th><th>Number<select><option value="mT5ONFScztzs" label="✅ Compatible" color="blue"></option><option value="jR9uGR5ecIA7" label="❌ Incompatible" color="blue"></option></select></th><th>Currency<select><option value="TqSjMvjusKIY" label="✅ Compatible" color="blue"></option><option value="fmXg8wSpkuOr" label="❌ Incompatible" color="blue"></option></select></th><th>Checkbox / boolean<select><option value="a1KIxolzQuMY" label="✅ Compatible" color="blue"></option><option value="nRV19vbBupqP" label="❌ Incompatible" color="blue"></option></select></th><th>Date / time<select><option value="rYARsw7sg0mj" label="✅ Compatible" color="blue"></option><option value="n8TfuJ3QCZf1" label="❌ Incompatible" color="blue"></option></select></th><th>JSON<select><option value="IsBASaKtOdun" label="✅ Compatible" color="blue"></option><option value="8kAqhjWn41tp" label="❌ Incompatible" color="blue"></option></select></th><th>Relation<select><option value="9hOA6VtiUygs" label="✅ Compatible" color="blue"></option><option value="aHdf1h6DamTs" label="❌ Incompatible" color="blue"></option></select></th></tr></thead><tbody><tr><td>Normal text</td><td><span data-option="HpRBofSXFHA5">✅ Compatible</span></td><td><span data-option="78DyTnPIRts4">✅ Compatible</span></td><td><span data-option="ppC0hWnlSnlO">✅ Compatible</span></td><td><span data-option="jR9uGR5ecIA7">❌ Incompatible</span></td><td><span data-option="fmXg8wSpkuOr">❌ Incompatible</span></td><td><span data-option="nRV19vbBupqP">❌ Incompatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>Rich text</td><td><span data-option="HpRBofSXFHA5">✅ Compatible</span></td><td><span data-option="78DyTnPIRts4">✅ Compatible</span></td><td><span data-option="ppC0hWnlSnlO">✅ Compatible</span></td><td><span data-option="jR9uGR5ecIA7">❌ Incompatible</span></td><td><span data-option="fmXg8wSpkuOr">❌ Incompatible</span></td><td><span data-option="nRV19vbBupqP">❌ Incompatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>URL</td><td><span data-option="HpRBofSXFHA5">✅ Compatible</span></td><td><span data-option="78DyTnPIRts4">✅ Compatible</span></td><td><span data-option="ppC0hWnlSnlO">✅ Compatible</span></td><td><span data-option="jR9uGR5ecIA7">❌ Incompatible</span></td><td><span data-option="fmXg8wSpkuOr">❌ Incompatible</span></td><td><span data-option="nRV19vbBupqP">❌ Incompatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>Number</td><td><span data-option="5YS9L34xs4mc">❌ Incompatible</span></td><td><span data-option="PFS2BxilCrgi">❌ Incompatible</span></td><td><span data-option="I1FgKECS1Ci0">❌ Incompatible</span></td><td><span data-option="mT5ONFScztzs">✅ Compatible</span></td><td><span data-option="TqSjMvjusKIY">✅ Compatible</span></td><td><span data-option="a1KIxolzQuMY">✅ Compatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>Currency</td><td><span data-option="5YS9L34xs4mc">❌ Incompatible</span></td><td><span data-option="PFS2BxilCrgi">❌ Incompatible</span></td><td><span data-option="I1FgKECS1Ci0">❌ Incompatible</span></td><td><span data-option="mT5ONFScztzs">✅ Compatible</span></td><td><span data-option="TqSjMvjusKIY">✅ Compatible</span></td><td><span data-option="nRV19vbBupqP">❌ Incompatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>Checkbox / boolean</td><td><span data-option="5YS9L34xs4mc">❌ Incompatible</span></td><td><span data-option="PFS2BxilCrgi">❌ Incompatible</span></td><td><span data-option="I1FgKECS1Ci0">❌ Incompatible</span></td><td><span data-option="mT5ONFScztzs">✅ Compatible</span></td><td><span data-option="fmXg8wSpkuOr">❌ Incompatible</span></td><td><span data-option="a1KIxolzQuMY">✅ Compatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>Date / time</td><td><span data-option="5YS9L34xs4mc">❌ Incompatible</span></td><td><span data-option="PFS2BxilCrgi">❌ Incompatible</span></td><td><span data-option="I1FgKECS1Ci0">❌ Incompatible</span></td><td><span data-option="jR9uGR5ecIA7">❌ Incompatible</span></td><td><span data-option="fmXg8wSpkuOr">❌ Incompatible</span></td><td><span data-option="nRV19vbBupqP">❌ Incompatible</span></td><td><span data-option="rYARsw7sg0mj">✅ Compatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>JSON</td><td><span data-option="HpRBofSXFHA5">✅ Compatible</span></td><td><span data-option="78DyTnPIRts4">✅ Compatible</span></td><td><span data-option="ppC0hWnlSnlO">✅ Compatible</span></td><td><span data-option="jR9uGR5ecIA7">❌ Incompatible</span></td><td><span data-option="fmXg8wSpkuOr">❌ Incompatible</span></td><td><span data-option="nRV19vbBupqP">❌ Incompatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="IsBASaKtOdun">✅ Compatible</span></td><td><span data-option="aHdf1h6DamTs">❌ Incompatible</span></td></tr><tr><td>Relation</td><td><span data-option="5YS9L34xs4mc">❌ Incompatible</span></td><td><span data-option="PFS2BxilCrgi">❌ Incompatible</span></td><td><span data-option="I1FgKECS1Ci0">❌ Incompatible</span></td><td><span data-option="jR9uGR5ecIA7">❌ Incompatible</span></td><td><span data-option="fmXg8wSpkuOr">❌ Incompatible</span></td><td><span data-option="nRV19vbBupqP">❌ Incompatible</span></td><td><span data-option="n8TfuJ3QCZf1">❌ Incompatible</span></td><td><span data-option="8kAqhjWn41tp">❌ Incompatible</span></td><td><span data-option="9hOA6VtiUygs">✅ Compatible</span></td></tr></tbody></table>

### Normal text

If a normal text field is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Normal text
* Rich text
* URL

#### Incompatible

* Number
* Currency
* Checkbox / boolean
* Date / time
* JSON
* Relation

### Rich text (HTML, Markdown)

If a rich text field is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Normal text
* Rich text
* URL

#### Incompatible

* Number
* Currency
* Checkbox / boolean
* Date / time
* JSON
* Relation

### URL

If a URL is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Normal text
* Rich text
* URL

#### Incompatible

* Number
* Currency
* Checkbox / boolean
* Date / time
* JSON
* Relation

### Number

If a number field is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Number
* Currency

#### Incompatible

* Normal text
* Rich text
* URL
* Checkbox / boolean
* Date / time
* JSON
* Relation

### Currency

If a currency field is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Number
* Currency

#### Incompatible

* Normal text
* Rich text
* URL
* Checkbox / boolean
* Date / time
* JSON
* Relation

### Checkbox / boolean

If a checkbox/boolean field is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Checkbox / boolean

#### Incompatible

* Normal text
* Rich text
* URL
* Number
* Currency
* Date / time
* JSON
* Relation

### Date/time

If a date/time field is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Date / time

#### Incompatible

* Normal text
* Rich text
* URL
* Number
* Currency
* Checkbox / boolean
* JSON
* Relation

### JSON

If normal text is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Normal text
* Rich text
* URL
* JSON

#### Incompatible

* Number
* Currency
* Checkbox / boolean
* Date / time
* Relation

### Relation

If a relation field is the source field, then the following are compatible/incompatible options to sync to:

#### Compatible

* Relation

#### Incompatible

* Normal text
* Rich text
* URL
* Number
* Currency
* Checkbox / boolean
* Date / time
* JSON
