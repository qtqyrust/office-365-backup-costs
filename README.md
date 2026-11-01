# office 365 backup: what Microsoft actually covers, what doing it right costs, and how to pick a plan that fits your storage

Most people searching for office 365 backup have already hit the unpleasant surprise: they deleted a mailbox or a batch of OneDrive files, contacted Microsoft, and were told the data is gone. That's not support being difficult. Under Microsoft's shared responsibility model, Microsoft maintains service resilience — uptime, redundancy, infrastructure security — while you remain responsible for protecting your data, accounts, and configurations. If a file gets deleted, corrupted by malware, or overwritten by a sync client, restoring it is your job.

This article covers three things: what Microsoft natively offers and where it falls short, what third-party backup actually adds (including a few limits vendors rarely mention), and what it costs — with a hosted Acronis option from Sharktech that starts at $4/month with 200 GB included, one of the cheapest entry points for a full Acronis Cyber Protect deployment you don't have to store yourself.

> **Quick take:** Sharktech's Acronis Cloud Backup starts at **$4/month (200 GB included)** or **$24/year — about $2/month** — with five data center locations and capacity scaling to 100 TB. One caveat before you click: Sharktech's public product pages describe the service as backup for servers, VMs, and cloud workloads, so if mailbox-level Microsoft 365 protection is your main goal, confirm supported workloads with their 24/7 team before ordering. 👉 [Check Sharktech's Acronis Cloud Backup plans and current pricing](https://portal.sharktech.net/aff.php?aff=1626&pid=648)

## Does Microsoft back up your Office 365 data?

Short answer: no, not in the way most people assume. Microsoft replicates your data across data centers so the *service* stays available, but replication copies whatever your data currently looks like — including corruption and deletions. Acronis's own documentation puts it bluntly: if a corrupted dataset makes it into Microsoft 365, the service will sync those corrupted files across accounts, leaving you with limited access, data loss, and — for businesses — potential compliance exposure.

Three native features people commonly mistake for backup:

- **OneDrive sync.** OneDrive holds a synchronized copy of your files. Delete something locally, or get hit by ransomware that encrypts local files, and that deletion or infection syncs to the cloud and every connected device. It's a sync tool.
- **Deleted items retention.** Exchange Online keeps deleted items for a limited period, after which they're gone. That's a grace window, not a recovery strategy.
- **Litigation hold and eDiscovery.** Built for legal compliance. Slow, admin-heavy, and never designed for "oops, restore my file."

That gap is exactly why Microsoft built its own backup service, and why a whole ecosystem of third-party tools exists around it.

## Your native option: Microsoft 365 Backup, and its real trade-offs

Microsoft's own backup service is genuinely capable in some respects, and it's worth understanding before you pay anyone else. Pricing is **$0.15 per GB per month** for protected data across Exchange Online, OneDrive, and SharePoint, with restore operations free of charge. Recovery points are frequent: every 10 minutes for recent periods on OneDrive and SharePoint, and across the most recent 52 weeks for Exchange. Restore speed is the headline selling point — Microsoft cites median rates of up to 1–3 TB per hour for large batches. Backups are immutable, stored on append-only blobs that can't be modified, and the data never leaves the Microsoft 365 trust boundary.

Retention is configurable in windows of 3 months, 6 months, 1 year, or 2 years, with 1 year as the default. Don't confuse that with "Microsoft keeps my data for a year no matter what" — it applies to backup recovery points you've enabled, and any restore window you pick eventually expires.

Two trade-offs get glossed over in most comparisons:

1. **Restore granularity.** Microsoft's service restores whole mailboxes, whole OneDrive accounts, and whole SharePoint sites. Per Acronis's comparison documentation, it does not support single-item restore, and it doesn't support cross-user or cross-organization recovery. Rolling back an entire site also overwrites everything after that point in time. If one employee needs three emails back from March, you're restoring a lot more than three emails.
2. **Where the copies live.** Because backups stay inside Microsoft's infrastructure, a tenant-level compromise — say, an attacker with admin credentials — touches both your primary data and your backups. Independent copies stored outside the Microsoft 365 boundary are the traditional answer to that scenario, and it's why the 3-2-1 backup rule hasn't died.

The per-GB cost also scales in a way worth modeling: at Microsoft's quoted rate, a tenant with 1 TB of protected data works out to roughly $150/month — an estimate based on the official $0.15/GB figure, not a plan price.

## What third-party Office 365 backup actually adds

Third-party solutions attack both gaps directly. Acronis, the platform behind the hosted option discussed below, makes a useful reference point. Its Microsoft 365 backup covers Exchange Online (user mailboxes, shared mailboxes, group mailboxes, public folders), OneDrive, SharePoint Online, and Teams data including channel files and team mailboxes. It backs up supported Microsoft 365 data up to six times per day, encrypts with AES-256, offers retention by date, by backup count, or indefinitely, and lets you configure an immutability period that protects backups from deletion — even by a compromised admin account. Recovery is item-level: single emails, files, and folders, with search and preview to locate them first, plus cross-user and cross-organization restore within the same Acronis tenant.

A couple of planning details most vendor pages skip. Workloads are counted with a conversion formula — **10 mailboxes = 2 teams = 2 sites = 1 OneDrive account** — and there are capacity ceilings per company (up to 50,000 protected workloads on Acronis's cloud agent, depending on the mix). If you're sizing a deployment, start with mailboxes, then OneDrive, then Teams, then SharePoint sites, in that order.

Two hidden limits apply to essentially any Exchange Online backup, and they change how you plan a recovery. Mailbox backups only capture user-visible folders; the Recoverable Items folder and everything under it (Deletions, Versions, Purges, Audits) is excluded. And restores don't auto-create missing objects — to restore a deleted SharePoint site, you first recreate an empty site manually, then point the restore at it. Neither is a dealbreaker, but both are better known before an incident than during one.

## Sharktech's Acronis Cloud Backup: all plans and pricing

Sharktech hosts the Acronis Cyber Protect platform as a managed service. You configure capacity and options in their client portal, backups run through Acronis's web console (independent of any server control panel), and their team handles the infrastructure — 24/7 support, with in-house engineering at every data center. The company has operated its own data centers since 2003 and, by its own materials, serves over 1,000 businesses across 73 countries. Storage scales from **200 GB to 100,000 GB**, and you pick a location: Los Angeles, Las Vegas, Denver, Chicago, or Amsterdam. An optional Files Sync & Share add-on turns the backup target into a shareable drive and is billed per GB on top — it's an extra, not part of the base plan.

Here's the full current pricing structure. Every cycle includes 200 GB of cloud storage, with per-GB rates for usage beyond that:

| Plan | Billing cycle | Price | Overage per GB | Buy |
| --- | --- | --- | --- | --- |
| Acronis Cloud Backup – Monthly | Monthly | **$4/mo** | $0.02 | [ Configure the monthly plan](https://portal.sharktech.net/aff.php?aff=1626&pid=648) |
| Acronis Cloud Backup – Quarterly | Every 3 months | **$8** (about $2.67/mo) | $0.04 | [ Configure the quarterly plan](https://portal.sharktech.net/aff.php?aff=1626&pid=648) |
| Acronis Cloud Backup – Semi-Annual | Every 6 months | **$12** (about $2/mo) | $0.06 | [ Configure the semi-annual plan](https://portal.sharktech.net/aff.php?aff=1626&pid=648) |
| Acronis Cloud Backup – Annual | Yearly | **$24/yr** (about $2/mo) | $0.12 | [ Configure the annual plan](https://portal.sharktech.net/aff.php?aff=1626&pid=648) |

The Files Sync & Share add-on runs $0.03 per GB monthly, $0.06 quarterly, $0.12 semi-annually, or $0.24 annually. Note that Sharktech's product page states your final recurring price depends on the capacity and protection options selected at checkout, and that additional security and disaster-recovery features depend on the chosen license — check the itemized price before confirming the order.

**The billing-cycle trade-off, stated plainly.** The longer the prepay cycle, the cheaper the base price and the higher the overage rate: monthly overage is $0.02/GB (about $20 per extra TB), annual is $0.12/GB — a 6x difference. That means the right cycle depends almost entirely on how predictable your storage is. A single server backing up a steady 250–300 GB is a clear case for annual: the base price drops by half and the overage you actually pay stays small. Backups that keep growing past a terabyte tip toward the monthly plan, where each extra GB costs six times less. If your storage is somewhere in between, run your own projection — divide your expected total storage by the overage rate for each cycle before committing. 👉 [Configure Sharktech's Acronis Cloud Backup with the cycle you pick](https://portal.sharktech.net/aff.php?aff=1626&pid=648)

## Who this plan fits — and who should look elsewhere

**A good fit if you:** want the Acronis platform (custom schedules, retention policies, file/folder/full-machine restores, encryption, anti-ransomware protection) without paying per-seat licensing or running your own storage; already rent a Sharktech server or VPS and want backups on the same bill; or prefer capacity-based billing that's easy to model, since Acronis's direct licensing is reported to run around $85 per device per year starting, storage not included. Sharktech says its hosted Acronis service costs about half what competitors charge, and the $4/month, 200 GB entry point is at least consistent with that claim. For a rough benchmark, another major host's managed Acronis offering starts around $11/month for 100 GB plus a base workload fee. Sharktech's version is self-serve by comparison — less hand-holding, lower price.

**The honest limitation, stated once more because it matters here:** Sharktech's public pages for this service list physical servers, VMs, and cloud workloads across Windows, Linux, and macOS. They don't list Exchange Online, OneDrive, SharePoint, or Teams among covered workloads. Acronis itself sells Microsoft 365 backup through dedicated licenses — "Acronis Microsoft 365 Backup" for service providers on monthly usage, or "Acronis Cyber Protect Advanced" for IT departments on annual subscriptions, with unlimited cloud storage on eligible per-seat plans — but whether that license is available through Sharktech's portal isn't stated publicly. Ask before ordering if M365 mailbox backup is the whole reason you're here.

**Alternatives in specific cases:** if you already own a Synology NAS, Synology's Active Backup for Microsoft 365 is a free add-on backing up unlimited accounts, limited only by your own storage — the trade-off is you buy, house, and operate the hardware. If item-level M365 restore with independent cloud storage is the priority and you'd rather buy direct from the platform vendor, Acronis's own Microsoft 365 plans cover Exchange Online, OneDrive, SharePoint, and Teams with granular, cross-user recovery. Neither gives you a hosted, capacity-priced Acronis deployment, which is the specific niche Sharktech fills. 👉 [See Sharktech's Acronis backup options and itemized pricing](https://portal.sharktech.net/aff.php?aff=1626&pid=648)

## FAQ

**How much does Office 365 backup cost?**
Three pricing models coexist. Microsoft's native Microsoft 365 Backup charges $0.15/GB/month with free restores. Acronis's direct Microsoft 365 plans use per-seat or per-workload licensing, with unlimited storage on eligible plans. Sharktech's hosted Acronis option bills by capacity, starting at $4/month for 200 GB with overage from $0.02/GB on monthly billing. Small tenants usually do best with capacity-based pricing; larger ones should price both models against their actual storage and seat counts.

**Can I restore a single deleted email?**
With third-party tools like Acronis, yes — individual emails, files, and folders restore without touching the rest of the mailbox, and cross-user restore is supported within the same tenant. Microsoft's native service restores whole mailboxes, accounts, or sites only, and overwrites everything after the chosen restore point on a full-site rollback.

**Is OneDrive version history enough?**
Version history helps with individual file rollbacks, but it does nothing for deleted accounts, ransomware that syncs encrypted files to every device, or retention windows expiring. It also keeps your only copy inside Microsoft's infrastructure. Reliable backup means a copy in a separate physical location or an independent cloud.

## Before you order: a short checklist

1. **Confirm workloads.** If Microsoft 365 mailbox backup is your priority, message Sharktech's 24/7 team first and ask which Acronis license and workloads their portal plan covers — the public page lists server/VM/cloud backup, and asking takes less time than a refund fight. Worth noting: Sharktech's pages don't publish a refund policy, so treat the first month as your trial.
2. **Pick the billing cycle by projected storage.** Stable workload around 200–300 GB → annual at $24. Storage expected to grow past a terabyte → monthly, for the $0.02/GB overage.
3. **Choose your data center** (LA, Las Vegas, Denver, Chicago, Amsterdam) if backup location matters for your compliance or latency situation.
4. **Plan a restore test.** Sharktech's own product page recommends making recovery testing part of your operating plan, and they're right: a backup you've never restored from is a hypothesis.

If you just need an affordable, managed Acronis deployment covering servers plus whatever workloads the license includes, the monthly plan is a low-commitment way to start, and annual cuts the cost in half once you're confident in your storage estimate. 👉 [Configure Sharktech's Acronis Cloud Backup](https://portal.sharktech.net/aff.php?aff=1626&pid=648) and confirm the final itemized price in the portal before checkout — two minutes of setup now beats explaining to the team why nobody kept a second copy.
