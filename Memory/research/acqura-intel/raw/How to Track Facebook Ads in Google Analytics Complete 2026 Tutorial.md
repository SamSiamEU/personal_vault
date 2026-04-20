**Uncover deeper insights into Facebook (Meta) ad performance with Google Analytics 4.**

While Facebook, now Meta, offers a valuable platform for advertising, its built-in metrics don’t capture the complete picture.

While it can help start user acquisition and track conversions, Facebook’s limitations become clear in its lack of understanding of user behaviour outside its platform.

This challenge is further amplified by the unreliability of third-party cookies, rendering solely relying on Facebook metrics an increasingly ineffective measurement strategy.

With a little help from Google Analytics, you can unlock valuable insights into how your Facebook campaigns influence website traffic, user behaviour, and ultimately, conversions.

In this blog, we’ll discuss:

💡 **Pro Tip**  
  
Google Analytics falls short in capturing the impact of ad views on revenue, and view-through attribution in Meta is fleeting due to the limitations around third-party cookies. Fortunately, impression attribution, like the one offered by Ruler, provides a solution. Analysing traffic patterns, Ruler reveals the hidden influence of ad views, even when users don’t click, and connects them to revenue.  
  
Explore the benefits of [**impression attribution**](https://www.ruleranalytics.com/blog/click-attribution/impression-attribution/) or [**book a demo**](https://www.ruleranalytics.com/book-demo) to see how it links your Facebook ad views to revenue.

## Why track your Facebook ads in Google Analytics?

Tracking your Facebook campaigns in Google Analytics is essential as it shows you how users are interacting with your website and provides a bigger picture of your customer journeys.

While you can get some basic information from Facebook about your website, it’s nowhere near as extensive as Google Analytics.

Facebook Ad Manager does a great job at telling you how many people saw and clicked on your ad but loses complete visibility of those individuals once they navigate away from the platform.

With Google Analytics, however, you can gather valuable demographic data from your Facebook ad campaigns and track customer behaviour, device functionality and more once a user lands on your site.

Also, with the latest iOS 14 update and the recent changes to the attribution settings, advertisers can now expect to see up to a [40% reduction of reported conversions](https://easyautotagging.com/facebook-apple-ios-14-privacy-update/) in Facebook Ads Manager.  
Thankfully, Google Analytics can deliver a lot of information on conversions, clicks and sessions to help improve the [performance of your campaigns](https://www.ruleranalytics.com/blog/inbound-marketing/measuring-marketing-performance/).

## How to track Facebook ads in Google Analytics

Effective marketing relies on understanding how your campaigns perform. Without data to guide you, your efforts are like shooting in the dark.

Google Analytics 4 allows you to track and analyse your Facebook ads, revealing valuable insights into how they drive traffic and user behaviour on your website. Here are four key steps to unlock this valuable data:

- Leverage URL campaign builder to get started
- Create a trackable link in Campaign Builder
- Add your trackable link to your Facebook ad
- Measure Facebook ads in Google Analytics 4

**💡** **Note:** For this guide, we’ll assume that you’ve already migrated over to your Google Analytics 4 account. If you haven’t, don’t worry. We have a complete guide on [how to get started with Google Analytics 4](https://www.ruleranalytics.com/blog/analytics/set-up-google-analytics-4/).

### 1\. Use URL campaign builder to get started

The first step to tracking your Facebook activity in Google Analytics is to generate a URL parameter for your ads.

**Related:** [How to track links with Google Analytics](https://www.ruleranalytics.com/blog/click-attribution/track-links-google-analytics/)

URL parameters provide more context and are the easiest method to measure and track your Facebook performance.

The best way to build your URL parameter is with [Google Campaign URL builder](https://ga-dev-tools.appspot.com/campaign-url-builder/).

![](https://www.ruleranalytics.com/wp-content/uploads/track-facebook-ads-google-analytics-campaign-builder-ruler-analytics.png)

Google’s Campaign Builder has various fields that you can use to track key information:

- Source: Where people found your ad. For example, Facebook, Google, email newsletter.
- Medium: Quantifies this type of traffic. This includes paid/CPC, organic and referral. Campaign medium is important, as it allows you to differentiate between your organic and paid clicks.
- Campaign Name: Gives unique labels to your campaigns, so you can easily track which ones are most effective in driving traffic or conversions.
- Term (Optional): Only relevant for Google Ads, this shows the exact keyword someone used to find your ad.
- Content (Optional): Useful for differentiating between multiple ads within a single campaign. For example, in a Facebook campaign with two ads, one video and one image, “content” could be “video” or “image” to see which performs better.

Once you fill out these fields, a campaign URL is generated. You can use this newly-generated URL to track Facebook traffic and conversions in Google Analytics.

But what should your UTM look like? Let’s go through it together.

**💡** **Pro Tip**  
  
Tracking social media channels like Meta and TikTok can be tricky, and relying solely on Google Analytics 4 won’t give you the full picture for measuring ad impact and making budget decisions. To get a clearer view of what’s actually working, it’s best to use a mix of methods – like first-party MTA, MMM, and incrementality. Our measurement framework shows how they all come together.  
  
**[Tap here to check out the framework for a better breakdown](https://www.ruleranalytics.com/resources/marketing-measurement-framework)**

### 2\. Define your source, medium and campaign variables

While URL Campaign Builder offers additional options, you only need a few key details to effectively track Facebook Ads in Google Analytics:

- Your website URL
- Campaign source
- Campaign medium
- Campaign name

These basic parameters suffice for tracking traffic and conversions in Google Analytics.

For advanced analysis, you can use additional fields like “campaign term” and “campaign content” to categorise your ad sets within the campaign and differentiate between different ad variations.

For now, we’re just going to focus on the mandatory fields in the URL Campaign Builder. In this example, we’re going to set up an ad for our marketing attribution product.

![](https://www.ruleranalytics.com/wp-content/uploads/facebook-ads-google-analytics-ad-placement-ruler-analytics.png)

First, we set up the URL. As we want people to book a demo, we’re going to copy and paste the URL to our marketing attribution product page. That way, users can click to learn more about the benefits of our solution before signing up for a demo.

Following this, we define the campaign source as ‘facebook’. Remember, UTM parameters are case-sensitive, so consistent lowercase usage across tags guarantees accurate data capture in Google Analytics.

Next, we specify the campaign medium as ‘paid’ for consistency with Google Analytics (which uses ‘cpc’ for paid search). Using ‘cpc’ here would mistakenly attribute social traffic and conversions to your paid search channels.

Lastly, we have “campaign name”. For clarity, we maintain consistency by using the exact name of your Facebook Ad campaign.

Once these fields are filled, this is what our trackable link should look like:

![](https://www.ruleranalytics.com/wp-content/uploads/facebook-ads-google-analytics-utm-ruler-analytics.png)

Now that we have our tracking link, it’s time to add it to our Facebook ad.

#### 3\. Add a trackable link to your Facebook ad

There are two ways you can add trackable links to your Facebook ads.

1\. The most common option is to copy and paste your whole URL in the “Website URL field”.

![](https://www.ruleranalytics.com/wp-content/uploads/facebook-ads-google-analytics-url-destination-ruler-analytics.png)

2\. The other option is to include your link in your ad copy. You can convert your URL into a short link using a tool like [Bitly](https://bitly.com/).

![](https://www.ruleranalytics.com/wp-content/uploads/facebook-ads-google-analytics-bitly-ruler-analytics.png)

Once you’ve shortened your link, it should look something like this:

![](https://www.ruleranalytics.com/wp-content/uploads/facebook-ads-google-analytics-text-placement-ruler-analytics.png)

### 4\. Measure Facebook Ads in Google Analytics 4

Your Facebook traffic will get pulled in automatically by Google Analytics 4 as long as you’ve set up your UTM codes correctly.

To check, go to **Reporting** > **Acquisition** > **Traffic Acquisition**.

![](https://www.ruleranalytics.com/wp-content/uploads/facebook-ads-google-analytics-traffic-sessions-ruler-analytics.png)

From the drop-down, change the channel group to view things like:

- session medium
- session source
- session source/medium
- session source platform
- session campaign

You can also use custom templates in Exploration to gain deeper insights into your Facebook Ad performance, such as:

- **Cohort Analysis:** Allows you to explore the behaviour of a group of users that came from a specific variable (source, campaign) over time on your app or website.
- **Funnel Report:** This allows you to see where Facebook visitors are dropping off in a conversion funnel. You can use the conditions to focus on specific campaigns or ads.
- **Path Analysis:** This allows you to track how Facebook users travel through your website and app with a tree graph.
- **User Behaviour:** This gives you valuable information about the people engaging with your site.

## Is Google Analytics really the best tool to track Facebook ads and conversions?

Google Analytics 4 isn’t always the best tool to measure your Facebook ads due to its inability to track individual visitors, limited attribution models and lookback windows, and, more importantly, its failure to account for ad impressions, the foundation of upper-funnel ads.

Let’s address some of the most common concerns raised by marketers:

1. Inability to track individual visitors
2. Limited attribution tracking
3. Doesn’t account for ad impressions

### 1\. Inability to track individual users and their first party data

Tracking conversions and traffic for Facebook is just the first step.

Turning those clicks and leads into deals and revenue is what matters most.

Due to privacy regulations and Google’s policies, visitor data collected through Google Analytics is anonymised.

This means you cannot track individual user journeys, leaving you with an incomplete picture of your advertising funnel.

While you can see how many users clicked an ad and landed on your site, the platform cannot tell you where those leads went afterwards, hindering your ability to assess their conversion into paying customers or valuable actions.

This anonymity, while crucial for user privacy, presents a challenge for advertisers wanting to demonstrate the revenue contribution of their ads.

### 2\. Limited attribution tracking

Google Analytics offers two attribution models for analysing Facebook Ads performance: Last-click and data-driven.

While last-click attribution might seem straightforward, it struggles to capture the complexities of today’s multi-touch customer journeys, often overemphasising the final touchpoint before conversion.

The alternative, data-driven attribution, leverages machine learning to assign credit more holistically, but its lack of transparency has raised concerns about how precisely credit is distributed.

Both models, however, share a crucial limitation.

They only consider conversions within the past 90 days. This can be a major drawback for businesses where customers take longer to make decisions, as valuable conversions from Facebook beyond this timeframe go misattributed, likely to Direct or organic search.

### 3\. Doesn’t account for ad impressions

Google Analytics doesn’t capture ad impressions, potentially underestimating the impact of upper-funnel campaigns like branding or display ads.

This leads to over-attribution of conversions to other channels, like organic search and direct, that might benefit from user exposure initiated by Facebook ads.

While Meta offers its view-through attribution metrics, their 24-hour window is often insufficient for B2B sales cycles, which typically stretch beyond a day.

Compounding the issue, Meta’s view-through attribution currently depends on third-party cookies, which are becoming more and more inconsistent.

## How to track your Facebook ad performance beyond Google Analytics 4

While UTM parameters offer a glimpse into how Facebook impacts website traffic and conversions, they miss the bigger picture.

Today’s tighter budgets and stakeholder demands for faster revenue growth require a deeper understanding of your Facebook ads’ true value.

Simply tracking website clicks isn’t enough. To truly gauge the effectiveness of your campaign, you need to understand its impact on your sales pipeline and ultimately, your revenue generation.

To achieve this comprehensive understanding, we’re employing the following 5 steps alongside UTM tracking in GA4.

- Capture qualitative data
- First-party MTA
- Impression modelling
- Incrementality testing

### Capture qualitative research

Qualitative research, often referred to as self-reported attribution, is a method that relies on prospects and customers voluntarily reporting how they learned about your product or service.

We capture qualitative research by:

- using a “how did they hear about us” field in our forms
- asking prospects on discovery calls what made them convert
- conducting surveys or focus groups with customers

Self-reported attribution has given us valuable insights into the effectiveness of both our advertising campaigns and dark social.

But, while self-reported attribution offers visibility over referrals, word of mouth, and social sources, it’s not perfect.

First, customers may not always remember or accurately report how they learned about a brand, particularly if they were exposed to multiple marketing channels.

Second, the data from self-reported attribution is often too vague. We did a study on it. [56% of the answers](https://www.ruleranalytics.com/blog/insight/self-reported-attribution/) from self-reported attribution were either low value or useless.

Overall, self-reported attribution is a good starting point, but eventually, you’ll need to explore more sophisticated tracking methods to gain a deeper understanding of your advertising performance.

### Track the click-path journey with first party attribution tracking

Using a first-party attribution tool, can help you understand the role your Facebook campaigns play in the overall customer journey.

We use Ruler to track website visitors (including those from Facebook) over multiple sessions and touchpoints. Whenever a visitor converts into a lead, Ruler connects the dots to create a customer journey.

![](https://www.ruleranalytics.com/wp-content/uploads//customer-journey-steps-ruler.png)

**Related:** [How to view full customer journeys with Ruler](https://www.ruleranalytics.com/blog/product/view-full-customer-journey/)

Ruler does this by capturing the FBCLID and [GCLID](https://www.ruleranalytics.com/blog/ppc/gclid-guide/) using first-party cookies. It then automatically sends the data we’ve captured on our Facebook leads to our CRM and other marketing tools.

This lets everyone in our business track where leads came from and determine which Facebook campaigns and ads are most valuable to your business.

> “ *Since the iOS changes, we’ve been relying on the data we get from Ruler way more. Lately, we aren’t getting the right data from Facebook ads portal, so I’m starting to use Ruler to make sure I’m not turning off ads that are actually working (an actual thing that’s happening). For businesses with high value/low quantity leads, this is so key,*” Kurt Dunphy, Growth Manager at Rally.”

As leads move from one stage to another, we keep a record of any changes in its dashboard.

With this data, we can spot any bottlenecks in advance and optimise our Facebook campaigns for optimum results.

When a lead is marked as closed as won, the revenue data is sent back to Ruler, allowing us to determine whether or not our ads are profitable and make changes as required to increase your returns.

Ruler also has a direct integration with Facebook. We can send MQLs, opportunities, and/or closed revenue back to Facebook as conversions to create targeted audiences and build more effective advertising campaigns to generate a higher conversion rate and ROI.

### 3\. Link ad views to revenue with impression attribution

While click-through attribution helps unveil hidden sources of traffic, it misses certain crucial interactions.

Imagine someone sees your Facebook ad, doesn’t click, but searches directly for your website weeks later and converts.

Click-based attribution misses this crucial interaction, leaving you unaware of the ad’s influence on their decision.

View-through attribution might seem like an alternative, but it really isn’t.

Its 24-hour window misses most real-world scenarios, and its reliance on third-party cookies jeopardizes its stability.

For a more comprehensive view, we use impression attribution and marketing mix modelling. It reveals how our Facebook campaigns, even without direct clicks, influence conversions and revenue.

Applying a machine learning-based Bayesian statistics model and Shapley value, Ruler develops sophisticated algorithms to match impressions to eventual conversions and revenue.

It offers a different perspective by illustrating how non-click interactions contribute to revenue, preventing the premature dismissal of upper-funnel channels that may prove effective.

MMM also provides essential insights for budget optimisation by simulating various scenarios to determine the most efficient allocation of marketing spend.

For example, it generates diminishing return curves, showing when additional spend no longer leads to a proportional increase in revenue. This allows marketers to identify the available headroom and predict potential upside.

![](https://www.ruleranalytics.com/wp-content/uploads/mmm-budget-allocation-dimishing-returns-ruler-analytics.png)

The statistical rigor and clear visual outputs from these models help secure buy-in, especially when past budget planning was based on rough estimates.

### 4\. Incrementality testing

Incrementality is the key to answering a critical question: Did this marketing campaign actually drive sales, or would those sales have happened regardless?

It’s an ideal approach to measuring the impact of Facebook ads, which as we already know, are notoriously difficult to track.

Considered the gold standard, incrementality isolates the true impact of your campaign, cutting through the noise and telling you precisely how much your marketing efforts made a difference.

One of the most effective ways to test incrementality is by dividing your audience into two groups: a treatment group exposed to your campaign and a control group that isn’t.

![](https://www.ruleranalytics.com/wp-content/uploads//incrementality-testing-ruler-analytics.png)

By comparing their behaviors, you can identify any significant differences, ensuring you’re measuring the campaign’s direct effect – rather than just correlating results with external factors.

Take a digital ad campaign, for example.

The treatment group sees the ad, while the control group does not. Any increase in behavior, like purchases or sign-ups, that occurs only within the treatment group can be attributed directly to the ad.

What makes incrementality even more powerful is its ability to validate findings from marketing mix models.

![](https://www.ruleranalytics.com/wp-content/uploads//triangulation-measurement-ruler-analytics.png)

While MMM is excellent for uncovering trends and forecasting long-term performance, incrementality testing cuts through the noise, pinpointing what’s truly driving results.

By combining insights from both approaches, marketers can differentiate between causation (what’s genuinely influencing outcomes) and correlation (what merely happens alongside marketing efforts).

💡 **Pro Tip**  
  
First-party MTA, MMM, and incrementality testing are essential components for gaining the most accurate insights and achieving the best possible results in your Facebook ad performance. For a deeper understanding of how to effectively triangulate these different forces, our comprehensive measurement framework can provide key guidance.  
  
**[Tap here to see the marketing measurement framework](https://www.ruleranalytics.com/resources/marketing-measurement-framework)**

## Start tracking your Facebook ads the right way

Tracking Facebook ads can be a tough gig due to the platform’s data limitations and changes in its ad tracking policies.

But by using a combination of first party MTA, marketing mix modelling and incrementality testing, businesses can gain valuable insights into the performance of their Facebook ads and optimise their marketing for maximum results.

With a tool like Ruler, you can’t go wrong. Ruler is a marketing attribution and MMM tool. So you can get the data you need to measure your Facebook ads from one single platform.

Learn more on how [Ruler attributes revenue to your marketing](https://www.ruleranalytics.com/blog/product/ruler-attribute-revenue/) or [book a demo](https://www.ruleranalytics.com/book-demo) and see it in action for yourself.

![](https://www.ruleranalytics.com/wp-content/uploads/ad-effectiveness-banner.png)

### Track Facebook in Google Analytics FAQs

**How to track Facebook ads in Google Analytics?**

To track Facebook ads in GA4, add UTM parameters to your ad URLs. These tags capture details like campaign name, source, and medium, letting GA4 group traffic and conversions properly. While GA4 doesn’t natively integrate with Facebook Ads Manager, UTM tracking ensures consistent data appears in your acquisition reports.

**How to add Facebook Ads data to Google Analytics?**

Facebook Ads data doesn’t flow automatically into Google Analytics. You’ll need to manually tag your ad links with UTM parameters. Once added, GA4 can capture data on traffic volume, sessions, and conversions from your Facebook campaigns. Make sure your UTM naming conventions are consistent, so you can easily analyse performance and attribute outcomes to specific campaigns, ad sets or creative within Google Analytics’ standard reporting views.

**How to check revenue from Facebook Ads in Google Analytics?**

GA4 will only show revenue from Facebook ads if you’ve set up eCommerce tracking or defined custom conversion events with values. However, that often misses leads that convert offline. Ruler Analytics links Facebook ad clicks to actual revenue outcomes using first-party data and integrations with your CRM. This helps you measure ROI more accurately, even for leads that convert via phone calls, emails, or in-store visits.

**What are the best practices for tracking Facebook Ads in Google Analytics?**

Use consistent, descriptive UTM parameters across all Facebook ads. Avoid generic labels like “paid\_social” unless you’re grouping ads intentionally. Always test URLs before publishing to confirm proper UTM tracking. Use lowercase throughout to avoid data fragmentation. While GA4 can handle the basics, many marketers pair it with a platform like Google Looker Studio or BigQuery for more advanced performance analysis and multi-channel attribution views.

**How to connect Facebook Ads with Google Analytics?**

Facebook Ads and Google Analytics don’t natively connect, so you must rely on UTM tracking. By tagging your Facebook ad URLs with UTMs, GA4 can categorise traffic and conversions accurately. Tools like Ruler Analytics can enrich this setup by linking ad clicks with leads, sales, and revenue, giving you a clearer picture of true marketing performance across platforms, not just within siloed reporting systems.

**What tools help with Facebook Ads and Google Analytics tracking?**

To go beyond UTM tagging, tools like Supermetrics and Funnel.io pull Facebook ad cost data into Google Looker Studio for visualisation. Ruler Analytics adds another layer, tracking users from Facebook ads through to conversions and revenue.

**How to measure Facebook Ads ROI in Google Analytics?**

GA4 can show ROI if you’ve assigned values to conversions, but this is typically limited to tracked web actions. It won’t reflect offline revenue or complex lead journeys. Ruler Analytics helps here by capturing Facebook ad clicks and matching them to closed deals in your CRM. It sends revenue data back into GA4 and ad platforms, giving you a more complete view of what’s working and where to optimise.