# Residential Proxy Services: How per-IP and per-GB billing works, and how to choose a plan for scraping, multi-accounting, and geo-targeted testing

Most people searching for residential proxy services stopped needing the definition a while ago. The definition is everywhere: real IP addresses on real home connections, so the site you hit sees a normal user instead of a datacenter range. The part nobody explains properly is the money. Two providers can advertise "from $0.68/GB" and "from $0.018/IP" and then bill you wildly different amounts for the identical scraping job, because they're selling different things.

This is a walk through how the billing models actually behave, what to check before you pay anyone, and a concrete price list from 9Proxy so you can see real numbers instead of "contact sales."

## What you're really buying

A residential proxy service rents you access to IP addresses that sit on consumer connections. That has three consequences worth understanding before you compare prices.

The first is that these IPs rotate out of existence. A residential IP is tied to someone's actual device, so it stays usable for a few hours up to roughly a day, not forever. What you're buying is a supply of addresses that refreshes, not a fixed server you can bookmark.

The second is price. Residential traffic costs far more than datacenter traffic because the supply comes from real devices and has to be maintained. Public price lists reflect that spread: Oxylabs charges $4.00/GB for residential pay-as-you-go, dropping to $2.00/GB at the 1,000 GB tier, while Bright Data's residential list price sits around $8.00/GB. Budget providers cluster between roughly $0.70/GB and $2.00/GB at higher volumes.

The third consequence is the one that trips people up: how you're charged changes with your workload, not just your vendor.

## Why the billing model matters more than the headline rate

Residential proxy services price in one of two ways, and sometimes both.

**Pay per GB** means every byte that moves through the proxy is metered. This is the default across the industry. It's flexible, you can rotate through the entire pool without worrying about IP allocation, and you can start small. It also hands your bill to page weight you don't control. Pull 100,000 product pages at 2–5 MB each and you've moved 200–500 GB in a month, which on a $3/GB plan is $600–$1,500 in proxy fees alone.

**Pay per IP** means you buy a fixed number of addresses and the traffic through them often isn't metered at all. 9Proxy's IP-based packages work this way: unlimited bandwidth on each purchased IP. Cost stops scaling with page size, and starts scaling with how many separate sessions you need running at once.

That distinction answers a question the "cheapest per GB" rankings usually dodge. If your job is heavy full-page capture on JavaScript-heavy sites, per-IP pricing insulates you from the one variable you can't forecast. If your job is light requests with heavy rotation, per-GB is normally the better fit because you're not paying for IPs you won't hold onto.

There's a third pattern worth knowing because it shows up in a lot of comparison tables: entry plan granularity. A provider with a 100 GB minimum will look terrible on a 5 GB job and completely ordinary at 100 GB. The same vendor can rank ninth and first on price without changing a single number. So before you pick the "cheapest" service, work out your realistic monthly volume and concurrency first.

## The checklist that predicts whether a service actually works

Price is the easy part. These are the items that decide whether the thing is usable in production.

- **Targeting depth.** Country-only targeting is not enough for price checks, ad verification, or SERP work where the city changes the result. You want at least state and city, ideally ZIP and ISP level.
- **Rotation control.** Rotating per request for broad collection, sticky sessions for anything with a login or a cart. You need both, and you need the sticky window to be configurable rather than fixed at 10 minutes.
- **Protocols.** HTTP/HTTPS is table stakes. SOCKS5 is what anti-detect browsers, `proxychains`, and a lot of Python tooling expect, so its absence forces ugly workarounds.
- **Authentication options.** Username/password suits cloud workers and scripts. IP whitelisting suits environments where you don't want credentials in config files.
- **What happens to dead IPs.** This is the real quality signal. Ask whether a non-working IP is replaced or credited, and within what window.
- **Support you can reach.** Ticket queues that answer in a day are fine for billing questions and useless when a target site tightens its detection layer overnight.
- **Integration path.** Whether the service drops into what you already run, or expects you to rewrite your stack around it.

One general warning: "unlimited bandwidth residential" is rare and usually comes with a fair use clause. Bright Data caps unlimited ISP proxies at 100 GB per proxy per month; Decodo's policy kicks in past 10 TB of total traffic or 25 GB per IP. Read the fair use policy, not the marketing headline.

## Where 9Proxy fits in this market

9Proxy is a residential-only provider with a pool of **20M+ residential IPs across 90+ countries** and targeting that reaches country, state, city, ZIP code, and ISP. It supports HTTP, HTTPS, and SOCKS5. Support runs 24/7 through Telegram, email, and a ticket system.

The company's positioning is now two models instead of one. IP-based packages give you unlimited bandwidth per IP with unused IPs that don't expire. GB-based packages bill purely on traffic, let you generate unlimited proxy endpoints, and carry a 180-day validity window, which is unlimited on Enterprise plans. A June 2026 pricing adjustment raised IP-based and bundle pricing; GB-based pricing was left untouched.

Operationally there are a few things in the docs that matter more than they sound. **Auto-Refresh** swaps out IPs that go offline, which stops long scraping jobs from dying on a connection error in the middle of a batch. **Auto-Rotation Proxy** changes IPs on a schedule you set per port, so you can bind specific ports to countries, cities, or ISPs and let different traffic groups follow different rules. Separate documentation notes a "Today List" that lets you reuse IPs from the previous 24 hours without paying for them again — useful for recurring checks on the same set of targets.

Two things 9Proxy is not: there's no datacenter or mobile product line, and IP-based packages require the desktop app because traffic is forwarded through a local port. GB-based plans run entirely from the dashboard.

Third-party scoring is mixed but reasonable. Review directories that track providers put 9Proxy around 3.9 out of 5, and it shows up in budget-tier comparisons next to DataImpulse as one of the cheaper options at roughly $1–2/GB effective rates.

👉 [Check current 9Proxy residential proxy packages and pricing](https://bit.ly/9-Proxy)

## The full package list, with real prices

Everything below is a one-time balance purchase, not a recurring subscription, which is why there's no "per month" column. USD, as published.

| Package | Billing model | What you get | Price | Effective rate | Validity | Buy |
| --- | --- | --- | --- | --- | --- | --- |
| 100 IPs | Per IP | 100 residential IPs, unlimited bandwidth | $24 | $0.24/IP | IPs never expire | [Get the 100 IP package](https://bit.ly/9-Proxy) |
| 500 IPs | Per IP | 500 residential IPs, unlimited bandwidth | $72 | $0.144/IP | IPs never expire | [Get the 500 IP package](https://bit.ly/9-Proxy) |
| 1,000 IPs + 500 bonus | Per IP | 1,500 residential IPs total, unlimited bandwidth | $126 | $0.084/IP | IPs never expire | [Get the 1,000 IP package](https://bit.ly/9-Proxy) |
| 2,500 IPs | Per IP | 2,500 residential IPs, unlimited bandwidth | $210 | $0.084/IP | IPs never expire | [Get the 2,500 IP package](https://bit.ly/9-Proxy) |
| 5,000 IPs | Per IP | 5,000 residential IPs, unlimited bandwidth | $360 | $0.072/IP | IPs never expire | [Get the 5,000 IP package](https://bit.ly/9-Proxy) |
| 15,000 IPs | Per IP | 15,000 residential IPs, unlimited bandwidth | $720 | $0.048/IP | IPs never expire | [Get the 15,000 IP package](https://bit.ly/9-Proxy) |
| 25,000 IPs | Per IP | 25,000 residential IPs, unlimited bandwidth | $863 | $0.035/IP | IPs never expire | [Get the 25,000 IP package](https://bit.ly/9-Proxy) |
| 50,000 IPs | Per IP | 50,000 residential IPs, unlimited bandwidth | $1,438 | $0.029/IP | IPs never expire | [Get the 50,000 IP package](https://bit.ly/9-Proxy) |
| 100,000 IPs (Business) | Per IP | 100,000 residential IPs, unlimited bandwidth | $2,300 | $0.023/IP | IPs never expire | [Get the 100,000 IP Business package](https://bit.ly/9-Proxy) |
| 200,000 IPs (Business) | Per IP | 200,000 residential IPs, unlimited bandwidth | $4,140 | $0.021/IP | IPs never expire | [Get the 200,000 IP Business package](https://bit.ly/9-Proxy) |
| 500,000 IPs (Business) | Per IP | 500,000 residential IPs, unlimited bandwidth | $8,625 | $0.018/IP | IPs never expire | [Get the 500,000 IP Business package](https://bit.ly/9-Proxy) |
| 5 GB | Per GB | 5 GB of residential traffic, unlimited endpoints | $15 | $3.00/GB | 180 days | [Get the 5 GB pack](https://bit.ly/9-Proxy) |
| 50 GB + 5 GB bonus | Per GB | 55 GB of residential traffic | $105 | $2.10/GB | 180 days | [Get the 50 GB pack](https://bit.ly/9-Proxy) |
| 100 GB | Per GB | 100 GB of residential traffic | $150 | $1.50/GB | 180 days | [Get the 100 GB pack](https://bit.ly/9-Proxy) |
| 200 GB | Per GB | 200 GB of residential traffic | $200 | $1.00/GB | 180 days | [Get the 200 GB pack](https://bit.ly/9-Proxy) |
| 1,000 GB | Per GB | 1,000 GB of residential traffic | $800 | $0.80/GB | 180 days | [Get the 1,000 GB pack](https://bit.ly/9-Proxy) |
| 2,000 GB | Per GB | 2,000 GB of residential traffic | $1,500 | $0.75/GB | 180 days | [Get the 2,000 GB pack](https://bit.ly/9-Proxy) |
| 3,000 GB (Enterprise) | Per GB | 3,000 GB, team mode, unlimited validity | $2,160 | $0.72/GB | No expiry | [Get the 3,000 GB Enterprise pack](https://bit.ly/9-Proxy) |
| 6,000 GB (Enterprise) | Per GB | 6,000 GB, team mode, unlimited validity | $4,200 | $0.70/GB | No expiry | [Get the 6,000 GB Enterprise pack](https://bit.ly/9-Proxy) |
| 10,000 GB (Enterprise) | Per GB | 10,000 GB, team mode, unlimited validity | $6,800 | $0.68/GB | No expiry | [Get the 10,000 GB Enterprise pack](https://bit.ly/9-Proxy) |
| Starter Bundle | IP + GB | 100 IPs + 5 GB | $30 | — | 180 days on traffic | [Get the Starter Bundle](https://bit.ly/9-Proxy) |
| Popular Bundle | IP + GB | 1,500 IPs + 50 GB | $180 | — | 180 days on traffic | [Get the Popular Bundle](https://bit.ly/9-Proxy) |
| Pro Bundle | IP + GB | 5,000 IPs + 500 GB | $720 | — | 180 days on traffic | [Get the Pro Bundle](https://bit.ly/9-Proxy) |

## Which package fits which job

The pricing table gets a lot simpler once you map it to real workloads.

**Light and occasional.** A price check across a few cities, a handful of SERP pulls, a competitor page you can't see from your own country. The 5 GB pack at $15 is enough, and the 50 GB pack at $105 is the jump most people make once they realize how much a JavaScript-heavy page actually weighs. Both give you unlimited endpoints, so you're not rationing IPs.

**Multi-account work and anything with a login.** Go IP-based. The 60-second-to-a-few-hours session behavior of a residential IP is the same on both models, but on per-IP billing you're not watching a traffic meter while a session stays open, and IPs you don't use stay in your balance indefinitely. 500 IPs at $72 is a sane starting point for a single operator; agencies managing hundreds of profiles should be looking at the 5,000 IP tier at $360.

**Heavy scraping with unpredictable page sizes.** This is the clearest case for per-IP. If your targets mix lightweight API responses with 5 MB rendered pages, a per-GB budget is a guess. Fixed pricing per IP removes that variable entirely. The 1,000 IP package with the 500 bonus IPs at $126 is the entry point most teams land on.

**Mixed workloads, one invoice.** The bundles exist exactly for this: stable IP access for account-bound tasks plus flexible traffic for broad collection. Starter at $30 for 100 IPs + 5 GB is priced to be tried. The Popular bundle at $180 covers a small agency with a few active clients.

**Teams and continuous infrastructure.** Enterprise GB plans drop the 180-day expiration and add team mode with one owner plus up to five members, per-member traffic controls, and activity logs. At 10,000 GB the effective rate is $0.68/GB. Zero expiration is the actual selling point here — it means an unused balance doesn't quietly evaporate while you plan the next quarter.

👉 [Pick a plan and generate your first proxy in the 9Proxy dashboard](https://bit.ly/9-Proxy)

## Three limitations to price in before you buy

**The desktop app requirement.** IP-based packages route traffic through 9Proxy's local forwarding client. That's fine on a workstation and awkward on a headless cloud server, where the app adds a moving part. If your scraping runs in containers, start with GB-based instead — it authenticates by username/password or IP whitelist straight from the dashboard.

**Freshness of IP-based inventory.** Residential IPs have natural uptime measured in hours, not weeks. A purchased IP isn't a permanent asset even though the balance never expires. Auto-refresh handles the failure case, but you should plan for rotation rather than assume a given IP will be alive tomorrow.

**The 180-day clock on GB packs.** Traffic in non-Enterprise GB plans expires six months after purchase. If you buy 2,000 GB for a project that slips, you may end up buying bandwidth twice. Match the pack size to your actual consumption rate rather than to the discount per GB.

## How to test without overpaying

Buy the smallest package that lets you run your real workload against your real targets for a few days. That's $15 on the GB side, $24 on the IP side, or $30 for the Starter bundle if you want to compare both models before committing.

Then do three things. Check geo accuracy by resolving a handful of proxies through an IP lookup tool and confirming country, city, and ISP match what you selected. Run your actual target sites and record success rate separately from site-side throttling, because they fail differently and blaming the proxy for a rate limit wastes a week. And pick a noisy target on purpose — if a provider's IPs are dragging reputations, it shows up fastest on the sites that ban aggressively.

If an IP doesn't connect, the documented policy credits it within the first minute, so report failures rather than eating them.

👉 [Create a 9Proxy account and run a small test batch](https://bit.ly/9-Proxy)

## FAQ

**Is 9Proxy residential or datacenter?** Residential only. The pool is 20M+ consumer IPs across 90+ countries, reachable over HTTP, HTTPS, and SOCKS5.

**Do I have to pay monthly?** No. Purchases are one-time balance top-ups. IP-based balances don't expire, GB-based packs last 180 days, and Enterprise packs don't expire at all.

**Per-IP or per-GB — which is cheaper?** Neither, in the abstract. Per-GB is cheaper if your traffic is light and you rotate constantly. Per-IP wins as soon as page weight or session length becomes hard to predict. The comparison only makes sense against your own volume.

**Can I target a single city or an ISP?** Yes — country, state, city, ZIP code, and ISP, with ports configurable so different task groups can run against different locations.

**Do unused IPs roll over?** They stay in your balance and don't expire. What doesn't roll over is a specific IP going offline, which is inherent to residential infrastructure rather than a billing choice.

## The short version

Residential proxy services are a market where the sticker price tells you very little. The two things worth spending your time on are matching the billing model to your workload and testing the pool against the sites you actually need to reach. Per-GB pricing suits light, high-rotation tasks; per-IP with unmetered traffic suits anything where bandwidth is unpredictable or sessions need to stay open.

9Proxy covers both, starting at $15 for 5 GB and $24 for 100 IPs, with geo targeting down to ZIP and ISP and no subscription lock-in. The honest recommendation is to start at one of those two entry points, point it at your real targets, and let the success rate decide — not the price per gigabyte on a comparison chart.
