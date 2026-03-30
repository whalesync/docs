---
description: >-
  Allowlist Whalesync's static outbound IP address to grant access to your
  databases and internal systems.
---

# Allowlisting Whalesync IP addresses

In some cases, access to your databases or internal systems from Whalesync may be blocked by your organization's network security settings. Whalesync uses a static outbound IP address for syncing data with your connected databases and services. Other operations, such as webhook callbacks, may not use this static IP and could still be affected by your network security settings even after allowlisting.

We recommend that your organization allows the following IP address:

```
34.66.3.22
```

## How to allowlist

### Cloud-hosted databases (AWS, GCP, etc.)

Add `34.66.3.22/32` to the inbound rules of the security group or firewall associated with your database instance.

### Supabase

In your Supabase dashboard, navigate to **Database Settings > Network Restrictions** and add `34.66.3.22/32` as an allowed address.

### Self-hosted / on-premise

Add `34.66.3.22` to your firewall's allowlist for the port your database is running on.

{% hint style="info" %}
If you have any trouble connecting after allowlisting, reach out to us via the in-app chat or at [support@whalesync.com](mailto:support@whalesync.com).
{% endhint %}
