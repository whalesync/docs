---
description: >-
  There are a few uncommon problems that you may encounter while using
  Whalesync. We're actively working on fixes, but in the meantime these are some
  workarounds.
---

# Known issues

### Images that are too large or have missing headers won't sync to Webflow

#### Issue

Webflow is very particular about what images it accepts and will silently fail to sync images that do not meet certain criteria. Specifically [images](https://university.webflow.com/lesson/image) can be synced to Webflow if:

1. They are less than 4 MB in size
2. They are configured correctly on the server with a known image [MIME type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) that has lowercase letters

#### Workaround

If your images are over 4 MB, you can make them smaller with image editing software to reduce their size.

If your images are hosted on a service that does not produce the correct MIME type, you may need to rehost your images on a service that does, such as [Cloudinary](https://cloudinary.com/).

### Images that were synced from Airtable are broken

#### Issue

When syncing images from Airtable to Bubble, Notion, or Postgres, the images appear to be broken after a few hours. This is due to a recent change in how Airtable exposes its image URLs. Now they expire, after which the URL won't work anymore.

#### Workaround

Please see [file-hosting.md](../../features/additional-features/file-hosting.md "mention") for details on making sure your base is set up to handle this.

### Airtable linked records, Airtable views, and record deletes in Webflow

#### **Issue**

If you're syncing an Airtable view to Webflow, if a record that was previously in the view is then removed from the view, Whalesync will sync that removal as a record delete. If that record is referenced by another table in Airtable via a linked record field and that field is synced to Webflow, Whalesync will be unable to delete the record in Webflow. You will see an error on the [issues](https://app.whalesync.com/issues) page: "This item is being referenced by another item in your CMS".

For example, let's say you have a "Published Blog Posts" Airtable view for a blog posts table and an "Authors" table that has a linked record field pointing to every blog post an author has written. One of your blog posts that was previously visible in the published view then is unpublished, hence disappearing from the view. The author still has a reference to that blog post in its linked record field. Whalesync will be unable to delete the blog post from Webflow as long as that reference exists in the linked record field.

#### Workaround

There are two possible workarounds (using the above example):

1. Create a new linked record field that only has a the blog posts in the "Published Blog Posts" view and sync that field to Webflow. You can use Airtable automations to dynamically update this field as blog posts come in and out of the view. Here is a [video showing the workaround](https://www.loom.com/share/8d802d34412a42b9b6027f54a70b24b1).
2. Update the linked record field on a one-by-one basis in either Airtable or Webflow to remove references to blog posts no longer in the view.

### Syncing more than 200 foreign keys to Bubble

#### Issue

Bubble's API has a restriction such that only 200 foreign keys (also known as record references or linked records) can by synced to Bubble in a single API request. The way Whalesync works today prevents more than 200 foreign keys to be saved to a Bubble foreign key field.

#### Workaround

You can create an [association table](https://en.wikipedia.org/wiki/Associative_entity) in Bubble. For example, let's say you have two tables, "People" and "Companies" and the Companies table currently has a foreign key that points to the People table.

Instead, you could create a "Companies\_People" table where each record has two fields: "company\_id" and "person\_id". In order to find all of the people a certain company is associated with, you can fetch all records from the Companies\_People table that has the desired company\_id.

