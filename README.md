# ScraperAPI Amazon Scraper: How It Works, What It Costs, Which Plan Fits You — Plus Real Credit Math, All Endpoint Types, and a Full Plan Comparison

If you've ever tried scraping Amazon on your own, you already know the story. You write a few hundred lines of Python, fire off your first batch of requests, and about twenty minutes later you're staring at a wall of CAPTCHAs, 503 errors, and IP blocks. Amazon's anti-bot infrastructure is genuinely impressive — not in a fun way. It's designed to make your life difficult, and it's good at it.

That's the gap ScraperAPI fills. It's a web scraping API that handles the miserable infrastructure side of things — proxy rotation, CAPTCHA solving, JavaScript rendering, automatic retries — so you just send a URL and get data back. For Amazon specifically, it goes a step further with dedicated structured data endpoints that skip the raw HTML parsing entirely and return clean JSON.

This guide covers everything worth knowing: how ScraperAPI's Amazon scraper actually works, what the credit system looks like in practice (including the parts the pricing page glosses over), which endpoint type fits which use case, how all the plans stack up, and what the real per-request cost works out to once you factor in Amazon's credit multiplier.

---

## Why Amazon Is Particularly Painful to Scrape Without Help

Amazon doesn't just block bad bots — it aggressively challenges anything that looks automated, including headers, browsing patterns, request frequency, and IP reputation. The countermeasures include:

- **Rotating CAPTCHAs** triggered by suspicious request patterns
- **IP-level blocking** targeting data center ranges (which is where most DIY scrapers originate)
- **JavaScript-rendered content** that requires a full headless browser to see
- **Region-specific pricing and availability** that changes based on where the request originates
- **Dynamic anti-bot signals** that evolve frequently, breaking scrapers that rely on static selectors

Building around all of this from scratch is a full-time engineering job. The alternative is routing requests through an API that has already solved these problems at scale.

---

## What ScraperAPI's Amazon Scraper Actually Does

ScraperAPI routes your requests through a pool of **40 million+ residential and datacenter IPs** spread across 50+ countries. For Amazon, it automatically handles JavaScript rendering and applies its Amazon-specific bypass logic — you don't configure any of this manually. You send a request; it sends back data.

Beyond raw HTML scraping, ScraperAPI offers **three dedicated Amazon Structured Data Endpoints (SDEs)** that return parsed JSON directly:

### 1. Amazon Product API

The most-used endpoint. You pass an ASIN (Amazon Standard Identification Number) and it returns a comprehensive JSON object with 18+ fields:

- Product name, description, and feature bullets
- Price and availability status
- All product images
- Ratings, review count, and all publicly available reviews
- Best Sellers Rank
- Product variants (color, size, etc.) with individual pricing
- Seller and shipping information
- Brand URL and store data

It supports **21 regional Amazon marketplaces** — `.com`, `.co.uk`, `.de`, `.co.jp`, `.com.au`, `.com.br`, and more — and accepts country-code targeting separately, so you can scrape `amazon.com` from a Canadian IP to get Canadian shipping data if needed.

### 2. Amazon Search API

Returns structured search results for any query on any supported Amazon marketplace. Useful for tracking product rankings, discovering competitors, monitoring keyword visibility, and building product catalogs.

### 3. Amazon Offers API

Pulls competitor offer listings for a given ASIN — third-party sellers, prices, fulfillment types (FBA vs. merchant-fulfilled), and seller ratings. Essential for competitive pricing intelligence.

All three endpoints are available **on every plan, including the free tier.** You don't need to upgrade to access structured Amazon data.

> 👉 [Start your free trial — 5,000 credits, no credit card required](https://www.scraperapi.com/?fp_ref=coupons)

---

## The Credit System: Where Most People Get Surprised

Every ScraperAPI plan gives you a monthly bucket of **API credits**. Every request burns some number of those credits — but not every request costs the same. This is the part most people don't fully absorb until they're mid-project wondering where their credits went.

**Amazon requests cost 5 credits each**, not 1. This is the baseline domain multiplier for all Amazon domains, applied automatically. You don't opt in — it's always there.

Here's how the full multiplier structure looks:

| Target Type | Base Credits per Request |
|---|---|
| Standard (blogs, news, plain HTML) | 1 |
| **Amazon (all endpoints)** | **5** |
| Google / Bing (and subdomains) | 25 |
| LinkedIn | 30 |

On top of the domain multiplier, optional parameters add more:

| Parameter | Additional Credits |
|---|---|
| `render=true` (JavaScript rendering) | +10 |
| `premium=true` (premium proxy pool) | +10 |
| `screenshot=true` | +10 |
| `ultra_premium=true` | +30 |
| `premium=true` + `render=true` combined | +25 (not +20) |
| `ultra_premium=true` + `render=true` combined | +75 (not +40) |
| Cloudflare / Datadome / PerimeterX bypass | +10 (auto-applied when detected) |

That last combination is where bills climb fast. Combining features costs **more than the sum of the individual parts** — a design choice that's documented but easy to miss. Anti-bot bypass credits are also applied automatically when detected, with no override option.

A few parameters carry **zero extra cost**: `country_code`, `session_number`, `device_type`, `wait_for_selector`, `output_format`, `keep_headers`, and `autoparse`. These are your free levers.

### What This Means for Amazon Scraping in Practice

If you're using the Amazon Product SDE with no additional parameters:

$$\text{5 credits per request} \times \text{100,000 credits (Hobby plan)} = \text{20,000 product lookups}$$

If you add JavaScript rendering on top:

$$\text{(5 + 10) credits} = \text{15 credits per request} \rightarrow \text{6,667 product lookups from the same plan}$$

The good news: ScraperAPI **only charges for successful requests.** A `200` or `404` response consumes credits; anything else (timeouts, 5xx errors) does not. For a scraping API, that's a meaningful consumer protection.

Unused credits do **not** roll over. They reset at billing renewal.

---

## All ScraperAPI Plans: Full Comparison

Here is every current plan with pricing, credits, concurrency limits, and geotargeting scope. Annual billing gives a flat **10% discount** across the board — applied automatically at checkout, no code needed.

| Plan | Monthly Price | Annual (per month) | API Credits/mo | Concurrent Threads | Geotargeting | Pay-As-You-Go |
|---|---|---|---|---|---|---|
| **Free** | $0 | — | 1,000 (permanent) | 5 | None | No |
| **Hobby** | $49/mo | $44.10/mo | 100,000 | 20 | US & EU only | No |
| **Startup** | $149/mo | $134.10/mo | 1,000,000 | 50 | US & EU only | No |
| **Business** | $299/mo | $269.10/mo | 3,000,000 | 100 | Global (50+ countries) | No |
| **Scaling** *(Most Popular)* | $475/mo | $427.50/mo | 5,000,000 | 200 | Global | Yes |
| **Professional** | $975/mo | $877.50/mo | 10,500,000 | 300 | Global | Yes |
| **Advanced** | $1,975/mo | $1,777.50/mo | 21,500,000 | 500 | Global | Yes |
| **Enterprise** | Custom | Custom | 22,000,000+ | 500+ | Global | Yes |

Purchase links:

- 👉 [Try the Free Plan (1,000 credits/month forever)](https://www.scraperapi.com/?fp_ref=coupons)
- 👉 [Get the Hobby Plan — $49/mo](https://www.scraperapi.com/?fp_ref=coupons)
- 👉 [Get the Startup Plan — $149/mo](https://www.scraperapi.com/?fp_ref=coupons)
- 👉 [Get the Business Plan — $299/mo](https://www.scraperapi.com/?fp_ref=coupons)
- 👉 [Get the Scaling Plan — $475/mo](https://www.scraperapi.com/?fp_ref=coupons)
- 👉 [Get the Professional Plan — $975/mo](https://www.scraperapi.com/?fp_ref=coupons)
- 👉 [Get the Advanced Plan — $1,975/mo](https://www.scraperapi.com/?fp_ref=coupons)
- 👉 [Contact Sales for Enterprise Pricing](https://www.scraperapi.com/?fp_ref=coupons)

**Things worth knowing that aren't obvious from the table:**

- **Geotargeting is gated.** Hobby and Startup are limited to US and EU proxies. Any project that requires country-level targeting in Asia, Latin America, or elsewhere needs at least the Business plan.
- **Pay-As-You-Go only unlocks at Scaling.** On Hobby, Startup, and Business, running out of credits mid-cycle means waiting for renewal or upgrading to the next tier. No overflow option exists below $475/month.
- **Analytics history is limited on lower tiers.** Hobby and Startup get 30 days of dashboard history. Business and above get unlimited.
- **The 7-day free trial** gives new accounts 5,000 credits (bumped from the standard 1,000 free plan) with no credit card required — enough to run meaningful tests against your real target URLs before committing to anything.

---

## How to Choose the Right Plan for Amazon Scraping

The honest answer is: it depends on volume, and the credit math above is your real guide. But here's a rough translation into plain use cases:

**Free trial or personal testing** — The 5,000 trial credits (7 days) or 1,000 permanent free credits are genuinely enough to validate whether ScraperAPI works for your Amazon targets. At 5 credits per Amazon request, that's 200 product lookups from the trial, which is a real sample.

**Small-scale monitoring or early-stage projects** — The Hobby plan at $49/month gives you 100,000 credits, which works out to **20,000 Amazon product lookups** per month at the base rate. For tracking a catalog of a few hundred products with daily refreshes, this covers it comfortably. Note the US/EU-only geotargeting limitation if your project needs other regions.

**Growing teams or SaaS products** — Startup at $149/month provides 1,000,000 credits — **200,000 Amazon product lookups** per month at base rate — with 50 concurrent threads. This is a meaningful operational tier for agencies or small products. Still US/EU only on geotargeting.

**Production infrastructure with global reach** — Business at $299/month is where global geotargeting unlocks, along with 3,000,000 credits (600,000 Amazon product lookups at base) and 100 concurrent threads. This is the first tier designed for real production workloads.

**High-volume or data-intensive operations** — Scaling and above add Pay-As-You-Go overflow so credit exhaustion doesn't hard-stop your pipeline, plus higher concurrency and priority support starting at Professional.

> 👉 [Compare all plans and start your free trial](https://www.scraperapi.com/?fp_ref=coupons)

---

## Real-World Performance: Where ScraperAPI Shines on Amazon

Independent benchmarks from Scrapeway (April 2026) put ScraperAPI's Amazon success rate at **98%** — one of the stronger figures in the industry for that specific target. Average response time clocked around 6.5 seconds per request, which is reasonable for a managed API handling proxy rotation and anti-bot logic server-side.

The structured data endpoints add a layer of reliability on top of that: rather than receiving raw HTML that your parser might misread after a layout change, you get a consistent JSON schema. ScraperAPI maintains the Amazon SDE parsing logic on their end — so when Amazon changes page structure (which it does frequently), the fix happens in their infrastructure, not yours.

That's not a trivial benefit. Maintaining Amazon scrapers in-house is a recurring engineering cost. Layout changes, A/B tests, and anti-bot updates can break a DIY scraper with no warning. With managed SDEs, that maintenance burden shifts.

---

## Using the Amazon Scraper: A Quick Look at the Integration

The API call itself is deliberately minimal. Here's a Python example using the Amazon Product SDE:

python
import requests

params = {
    'api_key': 'YOUR_API_KEY',
    'asin': 'B07FTKQ97Q',
    'tld': 'com',
    'country_code': 'us'
}

response = requests.get(
    'https://api.scraperapi.com/structured/amazon/product',
    params=params
)

print(response.json())


That returns a full JSON object with product name, pricing, reviews, BSR, images, variants, and seller info — no HTML parsing required on your end. The same endpoint works across all 21 supported Amazon marketplaces by changing the `tld` parameter.

For raw HTML scraping (when you need more control or want to parse the page yourself), the standard proxy-mode call works just as simply — you pass any Amazon URL as the target, and ScraperAPI handles the proxy routing and anti-bot logic automatically.

---

## What People Actually Think of It

ScraperAPI sits at **4.5/5 on Trustpilot**, **4.4/5 on G2**, and **4.6/5 on Capterra** with an ease-of-use score of 4.9/5 — that last number being the most consistent praise across platforms. The recurring sentiment is that setup is fast and documentation is clear enough to get running without support.

The recurring complaint is the credit math. Multiple reviewers mention that the gap between the headline credit number and the real request volume wasn't obvious until they were mid-project. One long-form analysis noted a case where a user purchased a plan expecting 60 million requests at 1 credit each, then discovered the 5x Amazon multiplier applied — effectively receiving 12 million usable Amazon lookups instead. The multiplier is documented, but it's not front-and-center on the pricing page.

The other honest limitation: performance is site-dependent. Amazon, Walmart, Zillow, and Etsy all show strong success rates. Instagram, Twitter/X, and Booking.com show 0% success in independent benchmarks — these are simply not supported targets, and no amount of premium proxy settings fixes that.

---

## The Discount Situation

There's no rotating promo code system to chase here. The simplest legitimate discount is annual billing, which cuts every plan by **10%** automatically at checkout. For the Hobby plan, that's $44.10/month instead of $49; for Business, it's $269.10 instead of $299. Over a year, that's real money saved without any code required.

For new users, signing up through a promotional referral link before subscribing is the standard way to lock in any active introductory offer.

> 👉 [Sign up now and claim your 5,000 free trial credits](https://www.scraperapi.com/?fp_ref=coupons)

ScraperAPI also has a **7-day no-questions-asked refund policy** — if you subscribe and the service doesn't work for your use case, you can get your money back by contacting support.

---

## Frequently Asked Questions

**Does the Amazon Structured Data Endpoint cost more credits than regular scraping?**
The Amazon SDE uses the same 5-credit base rate as any Amazon request. You're not charged extra for getting JSON instead of HTML — the credit cost reflects the domain, not the output format.

**Can I scrape Amazon product reviews with ScraperAPI?**
Yes. The Amazon Product API endpoint returns all publicly available reviews for a given ASIN automatically — no separate call required. Reviews are included in the same JSON response as product data.

**Which Amazon marketplaces are supported?**
21 regional TLDs: `.com`, `.co.uk`, `.ca`, `.de`, `.es`, `.fr`, `.ie`, `.it`, `.co.jp`, `.co.za`, `.in`, `.cn`, `.com.sg`, `.com.mx`, `.ae`, `.com.br`, `.nl`, `.com.au`, `.com.tr`, `.sa`, `.se`, `.pl`.

**What happens if I run out of credits mid-month?**
On Hobby, Startup, and Business, scraping stops until renewal. On Scaling and above, Pay-As-You-Go kicks in and you can continue at a fixed per-credit rate, with an optional spending cap to prevent surprise bills.

**Is there a free plan?**
Yes — 1,000 credits per month permanently, with 5 concurrent connections and no credit card required. New accounts also get a 7-day trial with 5,000 credits to test at a more realistic volume.

**Can I cancel anytime?**
Yes. Cancellation is available from the dashboard at any time, with no cancellation fees.

---

## Bottom Line

ScraperAPI is a practical tool for scraping Amazon at scale. The infrastructure — 40M+ IPs, automatic anti-bot bypass, structured JSON endpoints — genuinely solves the hard parts of Amazon data collection. The 98% success rate on Amazon in independent benchmarks backs that up.

The thing to go in clear-eyed about: the credit multiplier system means the headline plan numbers and your real request volume can be quite different. Amazon is 5 credits per request, not 1. Run your actual monthly volume through the credit math before choosing a plan. The free trial exists exactly for this — 5,000 credits against your real Amazon targets, no card required, and you'll know exactly what you're getting into before spending anything.

> 👉 [Start free — 5,000 trial credits, no credit card needed](https://www.scraperapi.com/?fp_ref=coupons)
