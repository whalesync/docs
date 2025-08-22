---
cover: ../../.gitbook/assets/gitbook-cover_wix.jpg
coverY: 0
---

# Wix CMS

## Wix CMS Connector Guide

This guide provides an overview of how to connect Whalesync to Wix CMS (also called Content Manager).

If you're unsure whether you're using Wix's CMS, review Wix's overview: [About the CMS (Content Manager)](https://support.wix.com/en/article/cms-content-management-system-an-overview). The CMS is for managing structured content in collections and powering dynamic pages. This is distinct from other Wix features like Wix Blog, Wix Forms, Wix Stores, Wix Bookings, Wix Events, or other Wix data sources.

### Connecting to Wix CMS

To connect your Wix CMS account to Whalesync, you'll authenticate using OAuth. This securely grants Whalesync access without sharing your password.

When you connect, you'll be redirected to Wix to approve the connection. As part of authorization, you must choose the specific Wix site you want Whalesync to access. After approving access to that site, you'll be returned to Whalesync to continue setup.

### Compatible fields

Whalesync does not provide full support for all fields in Wix CMS. If you need anything that is missing, please [reach out and let us know](../../resources/support/) to inform our planning.

| Field                     | Status                        | Notes                           |
| ------------------------- | ----------------------------- | ------------------------------- |
| Text                      | ✅ Fully supported            |                                 |
| Number                    | ✅ Fully supported            |                                 |
| Date                      | ✅ Fully supported            |                                 |
| Time                      | ✅ Fully supported            |                                 |
| Boolean                   | ✅ Fully supported            |                                 |
| Image                     | ✅ Fully supported            |                                 |
| URL                       | ✅ Fully supported            |                                 |
| Document                  | ✅ Fully supported            |                                 |
| Tags                      | ✅ Fully supported            |                                 |
| Color                     | ✅ Fully supported            |                                 |
| Reference                 | ✅ Fully supported            |                                 |
| Multi-reference           | ✅ Fully supported            |                                 |
| Javascript object & array | ✅ Fully supported            |                                 |
| Rich content              | ⚠️ Supported with limitations | Does not support embedded media |
| Media Gallery             | ➡️ Supported (1-Way)          | Read-only                       |
| Address                   | ➡️ Supported (1-Way)          | Read-only                       |
| Rich text                 | ✖️ Not supported              |                                 |
| Audio                     | ✖️ Not supported              |                                 |
| Video                     | ✖️ Not supported              |                                 |
| Multiple documents        | ✖️ Not supported              |                                 |

### Additional Fields

Whalesync adds special fields that are available to map in your sync but are not visible in Wix.

| Field Name    | Explanation                                   | Writable |
| ------------- | --------------------------------------------- | -------- |
| Wix Record ID | The unique identifier for an item in Wix CMS. | No       |
