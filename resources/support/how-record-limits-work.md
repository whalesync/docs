---
description: >-
  How Whalesync counts records against your record limit, how to manage your
  usage, and what happens if you go over.
---

# How record limits work

Every Whalesync plan includes a limit on the number of records you can keep in sync. This page explains how that count works, how to manage it, and what happens if you go over your limit.

## What counts toward your limit

Whalesync counts the records in your **active syncs** — syncs that have run at any point during the current calendar month.

A few things follow from this:

* **We don't double-count.** When the same records are kept in sync across the two sides of a Whalesync base, they're counted once, not twice. (See [How does Whalesync count records?](faq.md#how-does-whalesync-count-records) for a worked example.)
* **Records you aren't syncing don't count.** Bases, tables, or apps you've connected but haven't started syncing don't count toward your limit until they're syncing.
* **Paused syncs stop counting.** A sync that stays paused for an entire calendar month no longer counts the following month.

## The monthly reset

Your record count is based on a calendar month and resets at the start of each new month. Each month, only the syncs that were active _that_ month count toward your limit.

* A sync you keep running counts every month.
* A sync you leave paused for a full month drops out of your count the next month.
* A sync that was active for even part of a month counts for that whole month. (Pausing a sync at the very end of the month won't lower your count for that month — it still counted while it was on.)

## Freeing up room

There are two ways to reduce your record count:

* **Pause a sync** and its records stop counting **starting next month**. Choose this if you might want to turn the sync back on later — your configuration is kept, and you can resume anytime.
* **Delete a sync** and its records come off your count **immediately**. Choose this if you want relief in the current month and no longer need the sync.

You can also **upgrade your plan** at any time for a higher record limit.

## What happens if you go over your limit

If your synced records exceed your plan's limit, Whalesync will email you to let you know. You'll have time to get back under your limit — by pausing or deleting syncs you no longer need, or by upgrading your plan — before anything changes about your syncs.

If you're still over your limit after a series of reminder emails, Whalesync will pause your syncs. Your sync configurations are never deleted — once you're back under your limit or you've upgraded, you can re-enable your syncs from your dashboard.

## Getting back under your limit

To bring your usage back under your limit:

1. **See which syncs are using the most records.** Each sync's settings page shows how many records it's using, and a sync that isn't counting toward your limit this month is marked **Dormant**.
2. **Pause syncs you don't need right now** to free up room next month, or **delete** them to free up room immediately.
3. **Or upgrade your plan** for more headroom right away.

If your syncs were already paused by Whalesync, re-enable them from your dashboard once you're back under your limit.
