---
title: "UTM ID: Why You Must Include It in Your Ad Tracking"
source: "https://www.owox.com/blog/use-cases/utm-id"
author:
published:
created: 2026-04-20
description: "Without utm_id tag, you won’t be able to import ad cost data, impressions, and clicks for non-Google campaigns into Google Analytics 4."
tags:
  - "clippings"
---
If you have never heard of the *utm\_id* tag, now is the time to get to know it! Without this tag, you won’t be able to import ad cost data, impressions, and clicks for non-Google campaigns into Google Analytics 4.

##### [Find out the real value of ad campaigns](https://bi.owox.com/ui/signin/?_gl=1*1uumecq*_gcl_au*NTE4NDU1NDg1LjE3MzY4ODc1NDU.&_ga=2.87084058.360797677.1737324824-1597189560.1736887545)

Automatically import cost data to Google Analytics 4 from all your advertising services. Compare campaign costs, CPC, and ROAS in a single report and make fully-informed decisions.

![Get your free template now](https://i.owox.ua/pages/articles/41/41818.svg)

Start Free Trial

## What is UTM ID?

You are probably familiar with the [standard UTM tags](https://www.owox.com/blog/articles/how-to-use-utm-tags/) (*utm\_source, utm\_medium, utm\_campaign*), which are added to the end of a URL to track and analyze incoming website traffic.

***Utm\_id* tag** (which refers to the Campaign ID in Google Analytics) is not as widely-used.

UTM tags were invented by Urchin Software Corporation over 15 years ago. After Google acquired the company, this functionality was migrated to Google Analytics.

Although the *utm\_id* tag has been around as long as the standard of UTM tags, few people have used it until now. In Google Analytics Universal, this tag was optional and was primarily used to [shorten URL addresses](https://camptag.ai/resources/utmid-google-ads.html).

However, in Google Analytics 4, *utm\_id* has become more important. If you want to import ad cost data from non-Google advertising services to Google Analytics 4 through importing data, then four UTM\_tags [must be present](https://support.google.com/analytics/answer/10071305) in your ad campaigns:

- utm\_campaign (campaign name)
- utm\_source (campaign source)
- utm\_medium (campaign channel)
- utm\_id (campaign ID)

To be able to import non-Google advertising costs into Google Analytics 4, you need to go to your advertising accounts now and adjust the final URL by adding the *utm\_id* parameter.### Stop Rebuilding Reports Every Week

Model your logic once in SQL and reuse it everywhere. Automate refreshes and serve consistent answers across Sheets, dashboards, and AI workflows.

Try It Free

[View original](https://www.owox.com/app-signup)

[![Automate Business Reporting](https://cdn.prod.website-files.com/676a9690ef4ec151a6957187/67852095aa9f5797d7c3cccf_trial-v2.svg)](https://www.owox.com/app-signup)

## Why do you need to add utm\_id to your ad tracking?

Many marketers don't want to bother with manually creating complex reports and prefer to view advertising campaign reports in Google Analytics. But in order to evaluate the effectiveness of advertising, you need to upload expenses, impressions, and clicks from non-Google sources to Google Analytics. The problem is that without *utm\_id*, you won’t be able to upload this data to Google Analytics 4.

Let’s look at some specific examples.

After setting up ad cost data importing, a Non Google cost report will appear in the Acquisition section of Google Analytics 4.

![Google Analytics 4 report displaying Non-Google cost data with empty values for clicks, impressions, and cost metrics.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e4fa734f96b403de0e6_41795.avif)

Google Analytics 4 report displaying Non-Google cost data with empty values for clicks, impressions, and cost metrics.

To populate the columns for clicks, impressions, and expenses with values instead of zeros, you need to upload a CSV file with cost data into Google Analytics 4.

Let’s try, for example, to upload information about *campaign1* from *source/medium* = *bing/cpc* without a filled value in the *campaign\_id* column.

![Campaign data spreadsheet highlighting missing campaign ID.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e4f968cf26d7d60c9a0_41797.avif)

Campaign data spreadsheet highlighting missing campaign ID.

If we try to upload this file to GA4, the following error will appear: *Invalid empty value detected on row campaign\_id. A non-empty value must be set.*

![GA4 import error message showing 'Invalid empty value detected on row campaign_id' with import status failed.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e50e9894fd599357bcf_41799.avif)

GA4 import error message showing 'Invalid empty value detected on row campaign\_id' with import status failed.

If we fill in the *campaign\_id* field (with some random value), then when importing the file, we will see the following result:

![GA4 import history showing successful cost data imports with 100% imported and 0.0% match rate.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e4f6ed0de8bfe5faa9f_41801.avif)

GA4 import history showing successful cost data imports with 100% imported and 0.0% match rate.

If we look at the Match rate column, we’ll see zeros there. This means that GA4 cannot match the uploaded data with the information that is already in the system because there is no key (*utm\_id*) to blend the data.

The file is uploaded, there are no errors in it, but we have a zero % Match rate. This means that nothing we have uploaded in this file matches what is in GA4. All traffic that was not tagged with *utm\_id* will not be matched with what we uploaded in the file.

Therefore, you have not made any progress in analyzing the effectiveness of non-Google advertising campaigns in GA4 ¯\\\_(ツ)\_/¯

Many users ask themselves: *Why do I get a Match rate of 0% when importing cost data in Google Analytics 4?*

To solve the problem described above, you should first tag your traffic with *utm\_id*. The next day, in the report in the Google Analytics 4 interface, you will see that this field is no longer empty, which means that you did everything correctly.

Before:

![GA4 Non-Google cost report showing empty session campaign ID field.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e50a085c4f388fcec4f_41803.avif)

GA4 Non-Google cost report showing empty session campaign ID field.

After:

![GA4 Non-Google cost report showing populated session campaign ID field with user, session, and engagement data.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e4fb1f782ad1159570b_41805.avif)

GA4 Non-Google cost report showing populated session campaign ID field with user, session, and engagement data.

Next, you should fill in the corresponding *campaign\_id\_column* field in the uploaded file.

![Spreadsheet showing campaign data with the campaign ID column highlighted for completion.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e507c3930548bbdb226_41807.avif)

Spreadsheet showing campaign data with the campaign ID column highlighted for completion.

When you load this CSV file into GA4, the zero Match rate will disappear.

![GA4 import history showing successful and failed imports with varying match rates.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e4f8488b079b11b674b_41809.avif)

GA4 import history showing successful and failed imports with varying match rates.

And in the Non-Google cost report, you will see clicks, costs, impressions, and ROAS. 🎉😎

![GA4 Non-Google cost report showing clicks, costs, impressions, and ROAS data populated.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e50c1e80dc3e501bf28_41811.avif)

GA4 Non-Google cost report showing clicks, costs, impressions, and ROAS data populated.### Measure CPO And ROAS In GA4 With BigQuery

Collect clean ad cost data into BigQuery with OWOX. Then use GA4 Campaign Data Import to link costs to conversions and report true ROI across channels.

Start Free

[View original](https://www.owox.com/app-signup)

[![Measure CPO and ROAS in GA4](https://cdn.prod.website-files.com/676a9690ef4ec151a6957187/6786518ebbeae26df45b303f_trial-ga-v2.svg)](https://www.owox.com/app-signup)

## How to add utm\_id to your links

[Campaign URL Builder](https://ga-dev-tools.google/campaign-url-builder/) from Google can be used to create links with UTM tags.

![Google Campaign URL Builder interface with fields for creating UTM tagged links.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e4f642f1c5aa1388702_41813.avif)

Google Campaign URL Builder interface with fields for creating UTM tagged links.

### What should I use to fill in the Campaign ID value?

If you plan to manually upload expenses to Google Analytics 4, you can use any values you like for Campaign ID.

However, this approach won’t work for automated cost importing. The service that imports your ad cost needs to obtain the Campaign ID value. Not all advertising platforms allow you to retrieve this ID via an API. Therefore, we recommend duplicating the Campaign Name value in Campaign ID.

![Spreadsheet with campaign data, highlighting the campaign ID column and campaign name values.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e4fc164c823c4546d0b_41815.avif)

Spreadsheet with campaign data, highlighting the campaign ID column and campaign name values.

### How to check if utm\_id values are being passed to Google Analytics 4

To verify that you have set up your *utm\_id* correctly and that it is being passed to GA4, you can create a custom report in the Explorations section with the Session campaign ID parameter.

For example, if you have added *utm\_id* to your URLs and you already have traffic with these tags, then the *Session campaign ID* field will be populated in the report the next day.

![GA4 Exploration report showing Session campaign ID data, used to verify UTM ID values are being passed correctly.](https://cdn.prod.website-files.com/676a9690ef4ec151a69571ff/67958e5064d6ace6d0eae274_41817.avif)

GA4 Exploration report showing Session campaign ID data, used to verify UTM ID values are being passed correctly.

## Summary

If you plan to import advertising costs to Google Analytics 4, then you need to add [the required](https://support.google.com/analytics/answer/10071305) ***utm\_id*** parameter (campaign identifier) to your ad links.

We recommend updating [UTM tags](https://www.owox.com/blog/articles/how-to-use-utm-tags/) on all of your paid advertising campaigns to include the Campaign ID parameter, as this will be necessary to retrospectively import cost data into GA4.

Currently, only manual ad cost import is available in Google Analytics 4. To automate importing and save your time, use [the solution from OWOX](https://www.owox.com/import-advertising-costs-to-google-analytics-4/).

**Automatically import Google Analytics 4 cost data**

With OWOX, you can automatically merge your advertising cost data from different platforms and upload it to GA4 so you can analyze your return on ad spend (ROAS) and acquisition cost to make fully informed marketing decisions.

Early access will be available April 2023. Sign up now to get priority access, news, and updates.

![Data Analytics Platform Demo](https://cdn.prod.website-files.com/676a9690ef4ec151a6957187/67850cff2a0cb6c326cba32c_demo-girls-v2%402x.png)

### [Build Trusted Analytics With OWOX Data Marts](https://www.owox.com/demo/)

Define your logic once in your warehouse. Automate refreshes and deliver governed reports into Sheets and BI tools without messy handoffs.

Book a demo