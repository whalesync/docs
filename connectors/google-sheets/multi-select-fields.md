---
description: An explanation of how to set up multi-select fields in Google Sheets
---

# Multi-select fields

You can now use Whalesync to sync multi-select fields in Google Sheets. Multi-select allows you to store multiple values in a single cell, such as tags, categories, or any other list of options.&#x20;

### How to Set Up Multi-Select in Google Sheets

**Step 1:** Label the multi-select column

* Rename the column in your Google Sheet using the format: `multi_[column name]`. \
  &#xNAN;_&#x45;xample: If you're tracking tags, name the column `multi_Tags`._
* A multi-select "Frequented Cities" column is shown below.

<figure><img src="../../.gitbook/assets/Screenshot 2025-01-11 162758.png" alt=""><figcaption><p>Shows a multi-select field</p></figcaption></figure>

**Step 2 (optional):** Set the column as multi-select in Google Sheets

* In Google Sheets, navigate to **Data → Data Validation**.
* Set the column's data validation to allow multi-select.

<figure><img src="../../.gitbook/assets/Data Validation 2.PNG" alt="" width="346"><figcaption><p>Shows how to find the Data Validation menu</p></figcaption></figure>

**Step 3 (optional):** Add selectable options in the field

* Enter all the options you want to include in the multi-select field.
* Check the "Allow multiple selections" box if you want the field to be multi-select.
  * If the box is unchecked, the field will become a single-select field.
* _Tip: Highlight all the rows you want affected in the field **except** for the header (as shown below)._&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-01-11 162018.png" alt="" width="159"><figcaption><p>Shows selection criteria</p></figcaption></figure>

**Step 4:** Map the Table and Sync

* Complete the table mapping in Whalesync, then activate your sync.&#x20;
* Multi-select fields will appear as shown below.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-01-11 162501.png" alt=""><figcaption><p>Shows how Google Sheets multi-select fields appear in Table Mapping</p></figcaption></figure>







