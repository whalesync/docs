---
cover: ../.gitbook/assets/gitbook-cover_ms-dynamics.jpg
coverY: 0
---

# MS Dynamics CRM

## Supported Objects

<table><thead><tr><th>Tables</th><th>Status<select><option value="e06f8215296841cbb9b56300554bc898" label="✅ Supported" color="blue"></option><option value="26a18353ef33429b8325cf29bcbeeb54" label="➡️ Supported (1-way)" color="blue"></option><option value="17ee2063f0304528872db331d6c89a93" label="✅ Supported (as JSON)" color="blue"></option><option value="c915e2668c0b48a88fada9c39263f0c1" label="✖️ Not supported" color="blue"></option></select></th><th data-hidden></th></tr></thead><tbody><tr><td>👥 Accounts</td><td><span data-option="e06f8215296841cbb9b56300554bc898">✅ Supported</span></td><td></td></tr><tr><td>👤 Contacts</td><td><span data-option="e06f8215296841cbb9b56300554bc898">✅ Supported</span></td><td></td></tr><tr><td>📊 Opportunities</td><td><span data-option="e06f8215296841cbb9b56300554bc898">✅ Supported</span></td><td></td></tr></tbody></table>



## Things to Keep in Mind <a href="#h_bccce14d8a" id="h_bccce14d8a"></a>

### Deleting Accounts or Contacts is best done in MS Dynamics&#x20;

In MS Dynamics, when you delete an Account, all related Contacts and Opportunities are deleted as well. With the current way the MS Dynamics API is set up, if you delete an Account in Airtable or another synced connector, the corresponding Contacts and Opportunities will have their data erased, but the rows will not be deleted - they'll show up as empty rows.

The easiest way to fix this is to either:

* Delete the emptied rows in Airtable, or&#x20;
* Delete Accounts in MS Dynamics in the first place

{% embed url="https://www.loom.com/share/5d302f448e3a4eea95d285340719f164?sid=71e9d4d7-bd0b-41b1-be9f-69ff12ae6f5f" %}
