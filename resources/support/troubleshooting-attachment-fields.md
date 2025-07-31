---
description: >-
  What to do if attachments (e.g. images) aren't syncing between Airtable and
  Webflow
---

# Troubleshooting attachment fields

If, for some reason, images aren't syncing from Airtable to Webflow and there are no sync issues, here are steps you can take to help troubleshoot:

**1) Check if your images are >4mb**

Webflow rejects images that are >4mb and fails silently. If you make your image smaller than 4mb and upload it again, it should sync.

**2) Determine if it's a problem with the image field or the record in general**

Try duplicating the record in Airtable and seeing if the new record syncs.

* If the new record does not sync at all, it might be an issue unrelated to images.
* If the new record syncs, but without images then you know it's an image field-specific issue.
* If the new record syncs correctly, delete the original record.

**3) Try to isolate any "problem" images**

If you're syncing multiple images in an Airtable field, try removing them all and adding them back one by one. This can help you determine if there is any one image that is causing problems.
