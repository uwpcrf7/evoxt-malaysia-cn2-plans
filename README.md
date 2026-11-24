# Malaysia CN2 VPS: Which Evoxt Plan Is Enough, What the CN2 GIA Routing Actually Delivers, and Why the Same Plan Shows Two Different Traffic Limits (Full 11-Plan Price Table)

A Malaysia CN2 VPS from Evoxt starts at **$2.99/month** for the VM-0.5, and in late May 2026 the Kuala Lumpur optimized network finished a return-route rebuild: China Telecom goes home over **CN2 GIA (AS4809)**, China Unicom over **AS9929**, China Mobile over **CMI** direct. Finding that combination at three dollars is unusual.

What follows covers the parts that decide whether you buy: which of the 11 plans most people actually need, why the same VM-1 shows 1,000 GB of transfer in one review and 300 GB in another, what the upgraded routes measure from inside China, and whether the discount codes floating around still work.

> **Quick pick:** VM-1 at **$5.99/month** (1 vCPU, 2 GB RAM, 20 GB NVMe, 1 TB transfer on the Standard network) covers a WordPress site, a small API, or a lightly modded game server. If you only need a static site, a proxy, or a box to test in, VM-0.5 at **$2.99** is a real entry point, with the honest caveat that 5 GB of storage fills up fast.
> 👉 [Check the current VM-1 price and choose your network tier before checkout](https://bit.ly/EvoXt)

## All 11 Evoxt Malaysia plans and prices

Every plan below is the same hardware and the same price across Evoxt's Standard regions, which include Malaysia, Tokyo, the US, UK, Canada, Germany, Poland, Amsterdam and Australia. Weekly offsite backups, KVM virtualization, IPv6 and a 1 Gbps port are included on all of them, with no add-on charge for the backup.

| Plan | vCPU | RAM | NVMe | Transfer (Standard) | Price |
| --- | --- | --- | --- | --- | --- |
| [ VM-0.5](https://bit.ly/EvoXt) | 1 | 512 MB | 5 GB | 500 GB | $2.99/mo |
| [ VM-0.75](https://bit.ly/EvoXt) | 1 | 1 GB | 10 GB | 750 GB | $4.99/mo |
| [ VM-1](https://bit.ly/EvoXt) | 1 | 2 GB | 20 GB | 1 TB | $5.99/mo |
| [ VM-1.5](https://bit.ly/EvoXt) | 2 | 2 GB | 20 GB | 1.5 TB | $6.95/mo |
| [ VM-2](https://bit.ly/EvoXt) | 2 | 4 GB | 30 GB | 2 TB | $11.99/mo |
| [ VM-3](https://bit.ly/EvoXt) | 4 | 4 GB | 30 GB | 3 TB | $14.99/mo |
| [ VM-4](https://bit.ly/EvoXt) | 4 | 8 GB | 60 GB | 4 TB | $23.99/mo |
| [ VM-6](https://bit.ly/EvoXt) | 8 | 8 GB | 60 GB | 5 TB | $29.99/mo |
| [ VM-8](https://bit.ly/EvoXt) | 8 | 16 GB | 80 GB | 6 TB | $47.99/mo |
| [ VM-12](https://bit.ly/EvoXt) | 16 | 16 GB | 80 GB | 8 TB | $60.95/mo |
| [ VM-16](https://bit.ly/EvoXt) | 16 | 32 GB | 100 GB | 10 TB | $95.99/mo |

The transfer column is the Standard network quota. Evoxt sells the same plan names at the same prices on two other network tiers with less transfer, and the Malaysia node you are probably here for sits on one of them.

## The three network tiers, and why reviews disagree about traffic

This is the single most useful thing to understand before ordering, because it explains a contradiction you will hit within ten minutes of reading reviews. Evoxt sells Standard, Premium and Premium Plus networks under identical plan names. The CPU, RAM, disk and price match. The monthly transfer quota and the routing do not.

| Tier | Regions | VM-1 transfer | VM-16 transfer | VM-0.5 price |
| --- | --- | --- | --- | --- |
| Standard | US, UK, Canada, Germany, Poland, Amsterdam, Tokyo, Malaysia, Australia | 1,000 GB | 10 TB | $2.99 |
| Premium | Hong Kong, Osaka | not stated in the price tables reviewed | 5 TB | $2.99 |
| Premium Plus | Malaysia only | 300 GB per one plan table, 500 GB per a May 2026 review | 4 TB | $3.49 |

Two things worth noting. The Malaysia Premium Plus entry plan costs **$3.49**, not $2.99, so the headline price does not apply if you pick that tier. And the VM-1 quota on the Malaysia optimized network has been published as both 300 GB and 500 GB in different places; the console shows the live number at checkout, so treat any figure in a review as provisional.

The decision rule is short. Serving real traffic to people who are not in Asia? Take Standard and enjoy the 1 TB. Routing China and Southeast Asia traffic with latency as the priority? The optimized Malaysia tier trades roughly two-thirds of your transfer for better return paths. Serving Malaysian users on local ISPs? Premium Plus tightens the local peering further, and the smaller quota rarely matters for a local business site.

👉 [Compare the network tiers side by side in the deploy console](https://bit.ly/EvoXt)

## What the May 2026 routing upgrade changed

Older Evoxt Malaysia reviews describe CN2 for Telecom and call Unicom and Mobile "average". That was accurate before the upgrade. The current return paths from Kuala Lumpur are:

- **China Telecom:** AS149440 → CTGNet → CN2 GIA (AS4809)
- **China Unicom:** AS149440 → AS10099 → AS9929
- **China Mobile:** AS149440 → CMI, direct back to China

Outbound runs Telecom from the Guangzhou backbone through Hong Kong CTGNet into Singapore or Malaysia, Unicom via Hong Kong and Singapore on AS9929, and Mobile from the Shanghai backbone straight to Singapore or Malaysia.

Latency measured across 159 monitoring points in China:

| Route | Average latency |
| --- | --- |
| All China | ~92 ms |
| China Telecom | ~86 ms (Guangdong as low as 53 ms) |
| China Mobile | ~85 ms |
| China Unicom | ~109 ms |

Unicom is the laggard of the three at about 109 ms, which is still usable for SSH, admin panels and a website that Chinese visitors reach over Unicom. If your audience is mostly Telecom, the Guangdong figure tells you more than the national average: 53 ms from the south is close to what a domestic Hong Kong node delivers. A separate user test measured 70 ms elsewhere in Asia on the 1 Gbps port.

The data center behind this is AIMS KL 2, a Tier III facility in Kuala Lumpur, connected to MyIX and peered with local ISPs, Google and Cloudflare. Evoxt runs its own AS149440, which is why the return paths start with its own ASN rather than a reseller's.

## Hardware, and what "up to 6.0 GHz" really means

The CPUs identify as AMD EPYC Genoa (4th generation), reporting **4192 MHz** in test environments. Two sets of third-party benchmarks on different plans:

- **Geekbench 5, VM-0.5:** 1,293 single-core, 1,184 multi-core
- **Geekbench 6, Malaysia Premium plan:** 2,401 single-core, 4,203 multi-core
- **SysBench single-thread:** 4,792 in an April 2026 test, 4,800+ in a May 2026 test
- **Disk:** sequential read above 1,400 MB/s on NVMe

Those are two different tools and two different plans, so do not read the Geekbench 5 and Geekbench 6 numbers as a comparison of anything.

The "up to 6.0 GHz" figure in Evoxt's marketing is a maximum boost clock for the underlying hardware, not a sustained per-core frequency. Measured clocks sit around 4.19 GHz, which is still well above what the big clouds typically give you on a single core: AWS around 2.4 GHz, Azure and DigitalOcean around 2.3 GHz, Google Cloud around 2.2 GHz. For PHP execution, MySQL queries, Minecraft tick loops or a Node process, that gap shows up. On a 512 MB or 1 GB plan running a sustained all-core load, expect the sustained figure rather than the boost figure.

Independent testing backs the consistency claim rather than just the peak. VPSBenchmarks placed Evoxt second in its under-$25 category for 2025 and in the top three of that bracket for four consecutive years, and its February 2026 VM-1 test had the server accepting connections in under two and a half minutes.

## The real annual cost, including the fees nobody quotes

List price for VM-1 is $5.99/month, or $71.88 over twelve months. Evoxt advertises an automatic discount of roughly 10% on annual billing for NVMe VPS plans, no code required, which brings VM-1 to about **$64.69/year**, or roughly $5.39/month effective.

PayPal adds a **5.39%** processing fee, so paying that $64.69 by PayPal lands near $68. Credit card, Alipay and crypto (Bitcoin, Ethereum, Litecoin, USDt Tron) avoid that surcharge. Prepay terms run from monthly up to three years.

Resources can be added individually instead of jumping a whole tier:

| Add-on | Price |
| --- | --- |
| Extra IPv4 | $3/month each |
| Extra vCore | $3/month per core |
| Extra RAM | $2/month per GB |
| Extra transfer, Standard | $3 per TB |
| Extra transfer, Premium | $12 per TB |
| Extra transfer, Premium Plus | $24 per TB |

That transfer pricing is the trap worth flagging. Overrunning a Premium Plus quota costs eight times what the same overage costs on Standard. If your workload is bandwidth-heavy, do not buy the optimized tier and top up later.

Two policy details that surprise people: account credit is **non-refundable**, and one reported case had a VM suspended for exceeding its transfer quota, with service restored two days after the user purchased additional bandwidth. Set a bandwidth alert before you need it.

👉 [Start on monthly billing, then switch to annual once the plan fits](https://bit.ly/EvoXt)

## Discount codes: what is verified and what is not

Several codes circulate on coupon aggregators and GitHub review pages. None of them come from Evoxt itself, and at least one of those pages states plainly that Evoxt rotates codes periodically. Testing a code in the promotional field at checkout costs nothing.

| Code | Claimed discount | Where it comes from |
| --- | --- | --- |
| `EVOXT595` | 40% recurring, VM-1 and above | Third-party review page; a second page references the same 40% tier without the code |
| `AFF1129-hostspot` | 40% recurring | Third-party review page |
| `VPS25OFF` | 25% recurring | Third-party review page, described as the most widely cited |
| `AFF2261-btcvps` | 5% | Community listing |
| `BHW595` | Recurring, amount unstated | Hosting forums |

The 40% figure appears in two independent third-party write-ups, which makes it the most plausible of the bunch, but neither is official. If a code is rejected, the annual billing discount is the reliable fallback and it needs no code at all.

## Who should buy which plan

Match the plan to the workload rather than to the price ladder:

- **Personal blog or static site:** VM-0.5 at $2.99. Nginx with no heavy plugins; 512 MB runs a lean stack, not a cPanel stack.
- **WordPress, Laravel, a PHP app:** VM-1 at $5.99. Single-core clock speed does most of the work here.
- **Windows desktop over RDP:** VM-1 minimum, since Windows is only offered from that tier up. Evoxt does not charge a Windows licence fee, which elsewhere typically adds $10–20/month.
- **Vanilla Minecraft server:** VM-1.5 at $6.95 for the second core.
- **Modded Minecraft or a small multiplayer game:** VM-2 at $11.99.
- **Small API backend:** VM-2 or VM-3. Both have 4 GB RAM and 30 GB storage; the $3 difference buys two extra cores.
- **Anything serving Malaysian or Southeast Asian users:** Malaysia Premium Plus, where the MyIX and local ISP peering pays off.

Skip Evoxt if you need multi-threaded heavy compute, machine learning training, render farms, large-scale scraping, or instant support replies. The low tiers carry small transfer quotas and the ticket queue is not staffed for emergencies.

## The risks, stated plainly

Support tickets run **4 to 8 hours** at peak, with Telegram and community channels faster. Abuse detection is aggressive: Trustpilot reviews include a noticeable share of one-star ratings citing IP blocks and false positives, and an r/VPS thread describes a persistent connectivity failure with a disputed refund. Proxies, port scanning and services holding very high connection counts run into that system more often than a normal website or game server does.

For conventional hosting, a dev box or a game server, the risk profile is ordinary. For anything unusual, a month of VM-1 at $5.99 is a cheap way to find out before you prepay for a year.

👉 [Test a single month of VM-1 before committing to annual billing](https://bit.ly/EvoXt)

## Before you click deploy

Final selection rules, by situation:

- Cheapest usable box for a small site or proxy → VM-0.5, Standard network, $2.99/month
- One plan for most projects → VM-1, $5.99/month, 1 TB on Standard
- China-facing traffic where latency beats volume → Malaysia Premium Plus, accepting 300–500 GB on VM-1
- Windows RDP → VM-1 or higher, no licence surcharge
- More than one core needed for a game server → VM-1.5, then VM-2 for mods

Three things to confirm on the order screen, in this order: the network tier (Standard or Malaysia optimized, since that sets both your routing and your transfer quota), the promo code field (paste one, apply it, and check the discounted total before paying), and the operating system (Windows requires VM-1 or above). Everything else can be changed later; the tier you buy cannot be swapped as easily as a plan upgrade.

👉 [Open the Evoxt deploy console and pick your Malaysia network tier](https://bit.ly/EvoXt)
