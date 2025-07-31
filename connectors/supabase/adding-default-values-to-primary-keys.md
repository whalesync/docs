---
description: How to make your primary keys auto-generate values in Supabase
---

# Adding default values to primary keys

1. Click on the primary key in your table.
2.  Click "Edit column"

    <figure><img src="../../.gitbook/assets/1 (1).png" alt=""><figcaption></figcaption></figure>
3. Change the column type to uuid
4.  Set the Default Value equal to <mark style="color:red;">`gen_random_uuid()`</mark>

    <figure><img src="../../.gitbook/assets/2 (1).png" alt=""><figcaption></figcaption></figure>
5.  Make sure "Is Unique" is toggled on

    <figure><img src="../../.gitbook/assets/3.png" alt=""><figcaption></figcaption></figure>

