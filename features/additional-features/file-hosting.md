---
description: Details about Whalesync file hosting
---

# File hosting

## Overview

As part of the syncing process, Whalesync hosts files and attachments that you sync. For example, if you sync images in an Airtable attachment field, Whalesync temporarily hosts those images.

Whalesync URLs are intended for syncing purposes and not serving a live site. If you need long-term hosting, we suggest storing files in a service like [Supabase](https://supabase.com/docs/guides/storage), [ImageKit](https://imagekit.io/), or other cloud hosting providers.

File hosting happens in the background as part of the syncing process so you normally don't need to worry about the details. However, if you notice an issue with syncing files between services, please reach out to [support](../../resources/support/).

## Limitations

* Whalesync hosted files have a maximum size limit of 20 MB.
* Whalesync does not try to intelligently convert image formats or sizes. For example, if you upload an image in WebP format to Airtable and sync that image to another service that does not support WebP, Whalesync will not automatically convert the image to a supported type. You will need to convert the image to another type before uploading it to Airtable.
