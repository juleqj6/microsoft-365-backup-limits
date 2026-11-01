# office 365 cloud backup: what Microsoft actually protects, where it stops, and how to get an independent copy starting at $4 a month

Most people searching for office 365 cloud backup assume Microsoft is already backing up their email, files and Teams chats. In the way that matters after a real incident, it isn't. Microsoft guarantees that its infrastructure stays online, but the company's own shared responsibility model puts data protection on you. The native tools you get (retention policies, the two-stage recycle bin, and the newer Microsoft 365 Backup service) cover some scenarios and miss others, and the gaps show up at the worst possible time.

This guide walks through what Microsoft's native protection does and doesn't cover, what a proper third-party setup actually costs, and where a hosting provider like Sharktech fits in — including one honest caveat about its Office 365 support that most affiliate reviews won't tell you.

> **Quick verdict:** For most small teams, the practical move is a two-layer setup: protect your servers and VMs with Sharktech's Acronis Cyber Protect backup hosting, which starts at **$4.00/month** with no long-term contract, and keep an independent copy of large datasets on its S3-compatible storage at **$4.90/TB/month**. Before ordering, confirm with their 24/7 team exactly which Microsoft 365 workloads are covered — their product page lists servers, VMs and "cloud workloads" without naming M365 explicitly. 👉 [Configure Sharktech's Acronis backup service (from $4/month)](https://bit.ly/SharKtech)

## Why Microsoft 365 still needs a backup you control

The short answer: Microsoft runs the platform; you own the data, and only you are accountable for it.

This is the part of the shared responsibility model that gets glossed over in most vendor blogs. Microsoft ensures infrastructure uptime. It does not commit to protecting your data against accidental deletion, malicious insiders, ransomware that syncs through OneDrive, or an admin account getting compromised. Regulatory obligations around data retention and recovery — GDPR, HIPAA, FINRA, SOX and similar frameworks — land on the data owner, not on Microsoft.

Microsoft has narrowed the gap with its native Microsoft 365 Backup service, but the limitations are real and worth knowing before you rely on it:

- It does **not** support Microsoft Teams data.
- Granular, item-level recovery is currently limited to Exchange — SharePoint and OneDrive restore options are coarser.
- You can't customize backup schedules or recovery point objectives.
- Backups live inside Microsoft's own infrastructure. You can't choose a specific Azure region for them, and your primary data and backup copies sit in the same ecosystem, which is a single point of failure if that ecosystem has a bad day.

The two-stage recycle bin deserves its own mention, because it's what most people mean when they say "Microsoft already has backup." Deleted items survive there for a retention window, and it handles "oops, wrong folder" fine. It won't help when an attacker empties the recycle bin before encrypting everything.

That's the case for an independent copy: separate provider, separate infrastructure, separate credentials.

## Sharktech's backup services: the full current lineup

Sharktech is a Las Vegas-based infrastructure provider (21+ years in service, per its own site) that packages backup in two ways: managed Acronis backup hosting, and raw S3-compatible object storage you can point any backup tool at. There's no fixed tier ladder — the Acronis service is configured per capacity in their customer portal, and pricing is confirmed at checkout.

Here is everything currently shown on their site:

| Service | What it covers | Price | Billing | Buy |
| --- | --- | --- | --- | --- |
| Acronis Cyber Protect Backup Hosting | Physical servers, VMs, cloud workloads; Windows, Linux, macOS | From **$4.00/month** (final price depends on capacity + options at checkout) | Monthly, no long-term contract | [ Configure Acronis backup](https://bit.ly/SharKtech) |
| File Sync & Share (optional add-on) | File syncing and sharing layer on top of backup | Priced separately — itemized at checkout | Monthly | [ Configure with add-ons](https://bit.ly/SharKtech) |
| S3 Object Storage — 1 TB | Backups, archives, logs, media libraries | **$4.90/month** | Monthly; first 1 TB transfer included | [ Get S3 storage](https://bit.ly/SharKtech) |
| S3 Object Storage — 10 TB | Same, at scale | **$49/month** | Monthly | [ Get S3 storage](https://bit.ly/SharKtech) |
| S3 Object Storage — 100 TB | Same, high-volume archiving | **$490/month** | Monthly | [ Get S3 storage](https://bit.ly/SharKtech) |

Beyond 100 TB of storage or 300 TB of monthly transfer, pricing moves to a sales conversation. Backup plans can run daily or hourly, data is stored encrypted in an isolated environment, and Sharktech advertises 24/7/365 phone support plus a free consultation if you'd rather talk through sizing first.

One detail from their own product page that's easy to miss: File Sync & Share and additional protection options are **priced separately**, and the site explicitly tells you to check the itemized selection before confirming the order. The $4 starting price is the floor, not the total — your final recurring bill depends on the capacity and options you pick. That transparency beats an invoice surprise, but only if you actually look at the itemized list before clicking confirm.

## Can Sharktech back up your Office 365 mailboxes? The honest answer

Here's the caveat I promised, because this is exactly where a careless review would oversell.

Sharktech's Acronis product page describes protecting "physical servers, virtual machines and cloud workloads across supported Windows, Linux and macOS systems," and notes that application and database protection depends on workload support and licensing. It does **not** explicitly list Microsoft 365 — no Exchange Online, no SharePoint Online, no OneDrive, no Teams.

The underlying Acronis platform, however, handles Microsoft 365 thoroughly — this is verified from Acronis's own documentation, and it tells you exactly what to ask Sharktech for:

- Acronis's **cloud agent for Microsoft 365** is agentless and needs no local installation. It covers Exchange Online (user mailboxes, shared mailboxes, Kiosk mailboxes, litigation-hold mailboxes, group mailboxes and public folders), OneDrive accounts, SharePoint Online (classic communication sites and modern team sites, down to individual items), Teams (entire teams, channels, channel files, team mailboxes, meetings, team sites) and OneNote notebooks.
- Backups run up to **six times per day** on the cloud agent, with new users, groups, sites and teams automatically picked up by group protection plans. Cloud storage datacenters are deliberately located separately from Microsoft's datacenters — which addresses the "backup inside Microsoft's ecosystem" problem directly.
- A locally installed Acronis agent is much more limited: it backs up **Exchange Online mailboxes only** (user and shared), so if a provider hands you the on-prem agent version, Teams and SharePoint are out of scope.

So the right question for Sharktech's 24/7 team is precise: does their hosted Acronis licensing include the **cloud agent for Microsoft 365**, and which storage option does it use? That answer determines whether you get full M365 coverage or an Exchange-only setup.

Even within the fully featured setup, there are hidden limits that almost no comparison article mentions:

- Mailbox backups include only user-visible folders. The **Recoverable Items** folder (Deletions, Versions, Purges, Audits and related subfolders) is excluded.
- Restores cannot auto-create users, public folders, groups or sites. If a SharePoint site was deleted, you must manually create a new site first, then restore into it.
- The first full backup can take **days**, and Acronis documentation advises not starting the next backup before the previous one finishes. Microsoft's Graph API throttling can also slow backup schedules.
- The cloud agent caps manual backups at 10 per hour and concurrent restores at 10 per company, and protects up to 50,000 workloads per company — generous for small teams, worth knowing at enterprise scale.

None of these are dealbreakers for a typical business, but they shape your recovery plan, and it's better to know them before a disaster than during one. 👉 [Open Sharktech's backup configuration page](https://bit.ly/SharKtech)

## What third-party Office 365 backup actually costs

Most "best Office 365 backup" listicles stop at feature tables and never show you a realistic bill. Here are verified numbers.

**Sharktech's own pricing is capacity-based.** Acronis backup hosting starts at $4.00/month, and the recurring price scales with the backup capacity and protection options you select at checkout — there's no published tier table, so the checkout configuration is where your real number appears. The S3 storage side is simpler: $4.90 per TB per month, so 10 TB runs $49/month and 100 TB runs $490/month. The first 1 TB of monthly transfer is included; beyond that, transfer costs $0.90/TB.

**Buying Acronis direct costs more but names M365 explicitly.** Acronis's business Cyber Protect plans come in three tiers, starting at **$85.00, $109.00 and $129.00 per device**, each available with 1-, 3- or 5-year subscription terms — and it's the $109 tier that includes Microsoft 365, Google Workspace and email archiving. Acronis notes prices vary by region, reseller and subscription term. For individuals, True Image Advanced at $72.99/year includes Microsoft 365 backup with 50 GB of cloud storage, expandable to 500 GB; Premium goes to $124.99/year with 1 TB (up to 10 TB).

There's also a storage-model nuance inside Acronis itself that affects both cost and capability. Acronis offers a backup-to-storage option hosted **inside Microsoft's own trust boundary**: it covers Exchange Online mailboxes, OneDrive accounts and SharePoint sites with a fixed one-year retention, but only whole-mailbox/whole-site restores and no cross-user or cross-organization recovery. Its independent Acronis Cloud option adds Teams and Entra ID backup, flexible or indefinite retention, and granular item-level restore, licensed per seat with unlimited cloud storage. If a provider quotes you "M365 backup," ask which of these two models is behind it — the difference shows up the first time you need to recover a single email from a former employee's mailbox.

You can also combine layers: run server and VM backups through Sharktech's Acronis hosting at $4/month plus capacity, then push long-retention archives to the $4.90/TB S3 storage instead of paying per-device cloud storage premiums for cold data. If your retention window is measured in years, cold storage at under $5/TB changes the math considerably.

What you should *not* assume: that the $4 base price includes everything. Quoting Sharktech's own page: services start at $4/month, and "your final recurring price depends on the capacity and service options you select in checkout." Configure it, read the line items, then decide. 👉 [Check Acronis backup pricing and capacity options](https://bit.ly/SharKtech)

## How Sharktech compares with dedicated M365 backup vendors

If you want purpose-built mailbox-level protection, vendors like NAKIVO, AvePoint and UpSafe (listed in Microsoft's marketplace) compete in this space, and several support Teams data and granular Exchange, SharePoint and OneDrive recovery that Microsoft's native backup doesn't. Those products are built for exactly one job and generally price per user or per tenant.

Sharktech occupies a different spot in the market: general backup infrastructure at infrastructure pricing, sold without long-term contracts. Whether that's the right spot depends on your situation:

- **Dedicated M365 backup vendors** fit when your primary risk is tenant-level data loss (mailboxes, Teams, SharePoint) and you want restore tooling designed for that data model.
- **Sharktech's Acronis hosting** fits when you also have servers, VMs and endpoints to protect, or when you mainly need cheap, independent, S3-compatible storage as the third copy in your backup strategy.
- **Microsoft's native Microsoft 365 Backup** fits as a baseline, provided you accept the Teams gap, the Exchange-only granular recovery and the fact that backup copies live inside Microsoft's ecosystem.

It's also worth knowing what real users say about the underlying Acronis platform. A TrustRadius reviewer summed it up as: "It works great as a cloud backup solution, and restoring data from a past backup is easy" — while noting uncertainty about scaling past 50 devices. Recent G2 reviews (October 2026) praise centralized backup and reliable automation but flag a complex interface and hard-to-find policy settings. Known annoyances from TrustRadius reviews: SharePoint backups can pull in every user who has access to a site, and dormant users keep getting backed up and billed until you disable them. None of these are dealbreakers, but they're the kind of thing you learn after the purchase rather than before — unless someone tells you.

## Watch out for these S3 storage limits

Sharktech's object storage has one official restriction that matters for backup planning, and it's stated plainly on their own page: "This is a capacity-first object storage service, not an all-flash block-storage replacement."

In practice, that means it's excellent for exactly what an office 365 cloud backup strategy needs — backups, archives, logs, media libraries — but the wrong choice if you need a boot disk, filesystem semantics, or consistently low-latency block storage. The architecture is high-capacity HDD storage with an NVMe cache layer accelerating active data paths, exposed through an S3-compatible API. Features include versioning, object locking for immutable retention, lifecycle expiration rules, presigned URLs and multipart uploads — so immutability and retention automation are covered.

The other cost trap is transfer. You get 1 TB of monthly transfer included, then $0.90/TB. If you're doing large-scale restores or constant re-seeding of backup sets, factor that into your monthly total; at 10 TB of restore traffic in a bad month, that's roughly $8–$9 on top of storage. Worth knowing before a disaster recovery drill, not during one. 👉 [Review Sharktech's S3 storage pricing and limits](https://bit.ly/SharKtech)

## FAQ

**Does Microsoft 365 include backup for free?**
Partially. Native protection includes retention policies, the two-stage recycle bin, and the Microsoft 365 Backup service for SharePoint, Exchange and OneDrive. The gaps: no Teams support in native backup, granular recovery currently limited to Exchange, no custom schedules or RPOs, and backup copies stay inside Microsoft's infrastructure with no region choice.

**How much does independent Office 365 backup cost per month?**
With Sharktech, the Acronis backup service starts at $4.00/month plus capacity, with the final price confirmed at checkout, and S3-compatible storage runs $4.90/TB/month (1 TB included transfer, then $0.90/TB). For comparison, Acronis's direct business tier that includes Microsoft 365 starts at $109.00 per device per year, and consumer True Image Advanced with M365 backup is $72.99/year — prices vary by region and subscription term.

**Is Sharktech's backup service locked into a contract?**
No. Sharktech advertises its cloud backup services "without long-term contracts," and the Acronis service is billed monthly with pricing confirmed at checkout. Storage can be scaled up as retention windows and datasets grow.

**What should I check before ordering?**
Three things. First, ask their 24/7 support team whether the hosted Acronis licensing includes the cloud agent for Microsoft 365 (full coverage including Teams and SharePoint) or the local agent (Exchange Online mailboxes only), and which storage model backs it. Second, review the itemized optional services (File Sync & Share and extra protection options are priced separately). Third, plan retention honestly — their own guidance notes that more systems, longer retention and larger datasets all increase storage needs, so size capacity from your real data volume, not a guess.

## Which option makes sense for you

- **You only need an offsite copy of M365 exports and server backups, and you're comfortable configuring a tool like Rclone:** the S3 storage at $4.90/TB/month is the cheapest credible path, and you can start with 1 TB.
- **You have servers or VMs alongside your Microsoft 365 tenant and want one console for all of it:** start with the Acronis hosting at $4.00/month and add capacity as needed — it's billed monthly, so you're not betting on a multi-year contract.
- **You specifically need mailbox-level, Teams-aware M365 recovery with polished restore tooling:** a dedicated M365 backup vendor is the better-shaped tool; Sharktech is the better value when your protection scope goes beyond the tenant.

Before you click order on any of these, do two things. Write down what you're protecting, how long you need to keep it, and roughly how much data that adds up to — capacity pricing rewards people who know their number. And get Sharktech's answer on Microsoft 365 workload coverage in writing, so the scope you're paying for matches the scope you expect. When you've got that, 👉 [configure your backup capacity in Sharktech's customer portal](https://bit.ly/SharKtech) and confirm the full recurring price before committing.
