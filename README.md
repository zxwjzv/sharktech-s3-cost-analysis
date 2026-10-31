# online backup storage: what $4.90/TB S3-compatible storage actually gets you, and when a backup app like IDrive is the better buy

Most people searching for online backup storage want the same thing: an offsite copy of their data that survives a dead hard drive, a ransomware attack, or a coffee spilled on a laptop. What the search results rarely explain is that there are two completely different routes to that goal, and they suit very different people.

The first route is a consumer backup app — IDrive, Carbonite, Jottacloud and friends — where you install software, pick folders, and it handles everything. The second route is S3-compatible object storage, which you pair with a tool like Rclone or Restic and point at your own backups. It takes twenty more minutes to set up and can cost a fraction of the price at any real capacity.

Sharktech's S3 Object Storage sits squarely in the second camp: **$4.90 per TB per month, 1TB of transfer included, no per-request fees**, with no long-term contract. Whether that's the right pick depends entirely on which camp you're in, and that's what this article sorts out.

> **Quick picks**
> - **Want a "set it and forget it" desktop backup?** A consumer app is still the better route. IDrive's paid plans start at $3/year for 100GB, and Carbonite offers unlimited backup for one computer at $70/year. These are information only — the purchase links in this article go to Sharktech.
> - **Backing up more than a terabyte, or shipping backups from servers, NAS or CI pipelines?** S3-compatible storage is the cheaper road. Sharktech's Starter plan is $4.90/month for 1TB with 1TB of included bandwidth: 👉 [check Sharktech S3 Object Storage pricing](https://bit.ly/SharKtech)

## Two meanings of "online backup storage" — and why the difference matters

Online backup storage means keeping a copy of your files on remote servers so you can restore them after data loss. The confusion starts because the industry uses one phrase for two products.

A **backup service** (IDrive, Carbonite, Jottacloud) is an application plus storage. You designate folders or entire drives, the software duplicates them on a schedule, and the cloud copy sits independently of your machine — delete a local file and the backup copy stays. That's different from syncing, where deleting a file on one device deletes it everywhere. Backup services also tend to include extras like scheduling, versioning and mobile apps.

**Object storage** (Amazon S3 and its many S3-compatible competitors, Sharktech included) is raw storage with an API. There's no backup app bundled in; instead, you bring your own. Restic, Rclone, Duplicati, Nextcloud and dozens of other tools speak the S3 protocol natively, so you connect them to your storage endpoint and they handle the backup logic — deduplication, encryption, scheduling — while the storage just holds the bytes.

The practical consequence: if you have one laptop with family photos, the app route is easier and cheap enough. If you're backing up 4TB of VM images, nightly database dumps or a NAS full of media, the app route gets expensive fast, and a flat-rate per-TB storage bill starts looking very attractive.

## Sharktech's S3 Object Storage: plans, prices, and what's confirmed

Sharktech's object storage follows a deliberately simple model: one flat rate, no tiers, no bulk-discount cliffs. Storage and bandwidth are the only two line items on the invoice — no API request fees, no retrieval classes, no minimum storage duration.

Here's what the official product page currently shows:

| Plan | Storage | Monthly price | Bandwidth | Order |
| --- | --- | --- | --- | --- |
| Starter | 1 TB | $4.90/mo | 1 TB included | [ Order the Starter 1TB plan](https://bit.ly/SharKtech) |
| 10 TB | 10 TB | $49.00/mo | 10 TB included | [ Order the 10TB plan](https://bit.ly/SharKtech) |
| 100 TB | 100 TB | $490.00/mo | 100 TB included | [ Order the 100TB plan](https://bit.ly/SharKtech) |
| Custom | 100 TB+ or custom bandwidth | Linear at $4.90/TB | Per quote | [ Request a custom quote](https://bit.ly/SharKtech) |

A few things worth knowing before you pick a row:

- The **1TB Starter configuration is the one plan you can order directly from the live cart**, and it's the entry point Sharktech itself promotes. It comes with 1TB of included bandwidth.
- The 10TB and 100TB figures are the worked examples on the official product page, and they confirm the rate is genuinely linear: ten terabytes costs exactly ten times one terabyte, with no volume cliff. Third-party listings differ slightly on some mid-size configurations — one lists higher tiers at $5.00/TB rather than $4.90 — so the number that matters is the one in your cart at checkout.
- The rate stays the same whether you park 1TB or 100TB. There's no volume discount for committing to more capacity, which cuts both ways: small plans are cheap, and huge plans don't get cheaper per TB.
- **Bandwidth beyond the included amount is billed at $0.90/TB** per the official page. Note that Sharktech's own page carries slightly mixed wording on whether example prices already bundle that transfer, so treat checkout as the source of truth. If you need over 100TB of storage or 300TB of monthly transfer — or bandwidth allocations beyond the 1:1 ratio — the official page routes you to the sales team instead of the cart.

Under the hood it's high-capacity HDD with an NVMe cache layer in front, exposed through an S3-compatible API. That architecture is why the price per TB is low: you get HDD economics with the hot-path acceleration of flash, which is a sensible trade for backups where most data sits cold.

## What it actually costs compared to the big clouds

This is the part most "best online backup" roundups skip: the sticker price is rarely the whole bill.

Storing 1TB on Amazon S3 Standard runs roughly $23 per month, and pulling that same terabyte back out costs around $90 in egress fees. A restore-after-disaster scenario can cost more than a year of Sharktech storage. Sharktech's own FAQ puts it bluntly: "storage and bandwidth are the only two items on the invoice. No API request line items, no retrieval classes, no 'minimum duration' gotchas."

Here's how the S3-compatible field compares, based on 2026 published rates:

| Provider | Storage (per TB/mo) | Egress | Conditions |
| --- | --- | --- | --- |
| Sharktech | $4.90 | 1TB included, then $0.90/TB | None — month-to-month |
| Amazon S3 Standard | ~$23 | ~$90/TB | Per-request fees, storage-class management |
| Cloudflare R2 | ~$15 | $0 | Class A operation fees apply |
| Wasabi | $7.99 | $0 (fair use) | 90-day minimum storage duration |
| Backblaze B2 | $6.95 (raised from ~$6 in May 2026) | ~$10/TB (free via Cloudflare Bandwidth Alliance) | Daily egress capped at 3× stored volume |
| DigitalOcean Spaces | ~$20 | 1TB included, then ~$10/TB | Bucket-level granularity |

On raw storage cost, Sharktech undercuts every fully S3-compatible option in this comparison — roughly half of Wasabi's price and about a fifth of the big-three clouds. Wasabi and Backblaze B2 are close on price and have far larger communities and documentation libraries; if third-party tutorials matter to you, that's a real consideration, not a nitpick.

## The 10% recurring discount

Sharktech's S3 storage has a promo code floating around: **Y5YET1Z9EK**, listed by third-party reviewers as a **10% recurring lifetime discount** — it applies every billing cycle for as long as you keep the service, not just the first month. Applied to the Starter plan, that brings the effective rate to about **$4.41/TB/month**; a 10TB deployment drops from $49.00 to roughly $44.10/month.

Two honest caveats: this code circulates via third-party listings rather than Sharktech's own marketing pages, so apply it at checkout and confirm the discount shows in your cart before paying. And since it's a recurring code rather than a one-month trial, it's worth more the longer you stay.

👉 [Apply the 10% discount and order Sharktech S3 storage](https://bit.ly/SharKtech)

## When a consumer backup app is still the better buy

Raw price isn't everything, and for plenty of readers the traditional backup apps remain the smarter choice. The current landscape, based on published pricing:

- **IDrive** is the general-purpose pick in most recent roundups. Paid plans start at $3/year for 100GB, there's a free 10GB tier, and one account covers Windows, Mac, Linux, iOS and Android. Team plans are $11.99/month for 5TB and 5 computers, or $6.99/month for the first year on annual billing — then $9.99/month from year two. That first-year/second-year split matters: the discount applies only to year one, and only to new signups.
- **Carbonite** offers unlimited backup for one computer at $70/year and wins on simplicity — setup takes a handful of clicks. A New York Times review flagged two limits worth knowing: individual files need to be under 4GB, and private-key encryption was limited to Windows computers.
- **Jottacloud** has an unlimited plan at $120/year, though upload speeds are throttled after 5TB, and it lacks private-key encryption and incremental backups.
- **Arq Premium** runs $60/year and backs up five computers with your own encryption key.

These services charge more per TB — Carbonite's unlimited plan works for a single machine, but there's no economical way to park 10TB of archive data there. If you want phone backup, family sharing and a polished app, IDrive at these prices is hard to argue with. If you want bulk capacity, encrypted Restic repositories, or backups flowing automatically from servers, the app route has no good answer.

## The middle path: Sharktech's Acronis backup service

If you run a small business and want the polish of a managed backup product without becoming your own backup administrator, Sharktech also resells Acronis Backup Service, announced in January 2026. All plans include 200GB of cloud storage: **$4/month**, $8 per quarter, $12 per half-year, or $24 per year, with overages at $0.02/GB monthly down to $0.12/GB annually. It covers computers, phones and servers, handles encryption and compression, and can restore a single file or a whole system. File sync and sharing is available as an add-on at $0.03/GB monthly.

It's a niche offering — the 200GB baseline is modest — but for a handful of business endpoints with offsite compliance requirements, $24/year per account is a genuinely low entry point, and Sharktech pitches it at about half what competitors charge for equivalent Acronis coverage.

## Setting it up: the honest version

Sharktech's storage works with any S3-compatible tool, and the officially named integrations include Rclone, Cyberduck, Nextcloud, S3 Browser and direct API use; Restic and MinIO clients are also confirmed compatible across third-party listings. The setup flow for a typical encrypted backup:

1. Order a plan and grab your endpoint URL, access key and secret key from the customer portal.
2. Configure Rclone or Restic with those credentials and the endpoint — no code changes needed, since the API is S3-compatible.
3. Run your backup schedule as usual. Multipart uploads handle large objects, and integrity checks validate transfers.
4. Enable object versioning or object locking if you want ransomware-resistant immutable backups — both are supported features.

The bandwidth math works out neatly for this use case: nightly database dumps and incremental Restic repositories don't generate heavy restore traffic in normal operation, so the included bandwidth covers most backup workloads, and restores are the rare event you actually pay overage on.

What you give up: Sharktech has no built-in CDN edge network (you'd pair it with a separate CDN if you serve files publicly), no multi-region cross-continent replication with sub-millisecond consistency, and a much smaller community documentation footprint than Wasabi or Backblaze B2. If your priority is one-click integrations backed by hundreds of tutorials, the bigger names have an edge.

## FAQ

**Does Sharktech S3 storage have a free trial?** No free trial is published on the product page. Since plans are month-to-month with no contract, the cheapest way to evaluate it is a single month of the 1TB Starter plan at $4.90.

**What happens if I exceed my included bandwidth?** The official page lists overage at $0.90/TB of transfer. That's roughly 1% of what the same terabyte of egress costs on Amazon S3.

**Can I use my existing backup software?** If it speaks the S3 protocol — Restic, Rclone, Duplicati, Cyberduck, Nextcloud, S3 Browser, Jenkins and GitLab artifacts — yes, without code changes. Every mainstream backup tool with an "S3-compatible" destination option will work.

**Is there a real company behind this?** Sharktech has been in the infrastructure business since 2003, running data centers in Los Angeles, Denver, Chicago, Las Vegas and Amsterdam, with 24/7 support. As a measure of their platform quality, HostAdvice's independent review of their VPS product measured "6,000+ random IOPS, sub-millisecond network latency" — that's their broader infrastructure, not the object storage specifically, but it tells you the network underneath isn't a hobby operation. The object storage product itself is newer and less publicly battle-tested than the company behind it.

## Choosing between them, concretely

- One computer, photos and documents, want zero setup → an app like IDrive (from $3/year for 100GB) or Carbonite ($70/year, unlimited, one machine) fits; Jottacloud's $120/year unlimited plan covers heavier single users.
- A business that wants managed backups across devices without IT involvement → Sharktech's Acronis Backup Service from $4/month including 200GB.
- More than ~1TB, servers, NAS, CI artifacts, or encrypted Restic repositories → Sharktech's S3 Object Storage at $4.90/TB is the cheapest S3-compatible option on flat pricing, and the **Y5YET1Z9EK** code shaves a recurring 10% off if it's still active at checkout.

Two checks before you order any storage, Sharktech or otherwise: confirm the bandwidth overage rate and your plan's final price at checkout — that's where the surprise line items live on hyperscaler bills — and run one full restore test in your first month. A backup you've never restored from is a hope, not a backup. If the numbers above match what you need, 👉 [order Sharktech S3 Object Storage starting from the 1TB Starter plan](https://bit.ly/SharKtech) and point your first backup at it tonight.
