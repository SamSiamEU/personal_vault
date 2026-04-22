![How to use the Meta ad library API to scrape ad data? - Blog post banner image for Swipekit](https://swipekit.app/blog/articles/meta-ad-library-api/banner.jpg)

Using the Meta API for direct access means you can play with the API and write code that quickly fetches results for specific ads, competitor research and run your own bulk analysis with an LLM.

Why should you follow this guide?

I run Swipekit, a tool to save ads from the Facebook ad library. We've been working with the ad library for over 3 years now.

So I definitely know a thing or two about working with the ad library's API:)

Before we start off, there are two big caveats:

1. The API only works for the ads running in the European Union, Brazil(limited scope) or if they are tagged as political/social cause ads.
2. The Ad library's API won't return information such as ad assets, advertiser info, etc. That can be fetched via scraping, which deserves its own article and I'll cover that in the future.

Now that we've cleared the gotchas, let's roll.

Contents

- What data access is available?
- How to get access to the Meta API?
- Working with the Meta API

## What data access is available?

Technically Meta give out 3 ways to access their data(apart from the Ad library):

Reports: These are more so for researchers. You can narrow down by advertiser(brand) and date range and Meta will give you a csv of data. However in practice I haven't found it much useful since it doesn't give out data for non-political/social issue brands.

API: We're gonna focus on this today, stay tuned!

Branded content: This is for finding influencer posts, eg content creator in collaboration with brand promoted x. This deserves its own topic.

![Meta ad library data](https://swipekit.app/blog/articles/meta-ad-library-api/body-1.png)

For our usecase, we're gonna use the API access today. This is great for getting insights on brands and let's us get their targeting information, reach and other juicy metrics.

![Example of an ad JSON fetched using the meta ad library api](https://swipekit.app/blog/articles/meta-ad-library-api/body-2.png)

Here's an ^ [example of a ad fetched using the api.](https://gist.github.com/shash7/192ed6ba090855e2eb61ac642e56adc6)

Let's get started!

## How to get access to the Meta API

To start using the Meta API, you'll need two things.

1. A app inside the Meta developers console. You can get started from [here](https://developers.facebook.com/apps/).
2. Verify your identity. This is only a requirement to access the API endpoints required for the ad library.

Technically it doesn't matter what steps you do this in, however I recommend you get started with creating your Meta app first as that can be daunting for first time users.

### How to create a Meta app for Ad library access

First, head over to the [https://developers.facebook.com/apps/](https://developers.facebook.com/apps) and click on 'Create App' in the top right corner.

![Meta create app process](https://swipekit.app/blog/articles/meta-ad-library-api/body-3.png)

It doesn't matter much what details you enter. In the usecases section, you can put down 'Create app without a usecase'.

Your app type can be consumer.

### How to verify your identity for ad library API access

Head over to the [verification pag](https://www.facebook.com/ID) e and start your verification process.

You'll be asked to give proof a identification, eg, driver's license. Upload the file and within a few days you'll be given access(I believe it took me a few hours)

![Meta ad library verification](https://swipekit.app/blog/articles/meta-ad-library-api/body-4.png)

Once you complete these steps, you'll have access to the ad library specific API endpoints!

To verify if you have access, head over the the [Fb graph explorer tool](https://developers.facebook.com/tools/explorer) and set your app in the sidebar.

Then enter a query, for example:

ads\_archive?ad\_reached\_countries=AU&search\_terms=sand

Then enter ads/library/ and click on 'Send'. If something comes up in the middle of the screen, you're good.

![Check Meta ad library access via the Graph API tool](https://swipekit.app/blog/articles/meta-ad-library-api/body-5.png)

For the next steps, you'll need a access token. For now you can utilize the access token provided inside the Graph explorer page(the one above the 'Generate Access Token' button.

## Working with the Meta API

Ok now comes the hard part. The ad library api is extremely wonky to work with. Notably, there's one major shortcoming - you can't search by ad's id.

Luckily there's a workaround. Let's cover some basic ground first.

### Understand pageId and adId

You'll be primarily working with 2 IDs:

adId: This id uniquely identifies an ad inside the ad library. Think of this as the primary ID.

pageId: This id is used for pagination inside the ad library. Think of it as the cursor ID. While not directly useful, we need this to get specific ad's data.

Unfortunately the pageId isn't directly exposed in the UI. Read below on how to get the pageId.

### How to get the pageId?

There are two ways to get the pageId of an ad

1. View the ad's individual page and infer the pageId from the url parameter.

To do this, copy the ad's unique url(you can do this by clicking the 3 dots on the ad card and then clicking on 'copy ad link'.

![facebook ad library copy ad link](https://swipekit.app/blog/articles/meta-ad-library-api/body-6.png)

Then paste the url in a new tab and then copy the last parameter of the url(view\_all\_page\_id)

![facebook ad library get pageId](https://swipekit.app/blog/articles/meta-ad-library-api/body-7.png)

2. Use the Swipekit extension to get the pageId

This is a super simple method to get the pageId quickly.

You don't need to have a Swipekit account to get the pageId, just install the [Swipekit chrome extension](https://chromewebstore.google.com/detail/ad-library-downloader/gojmmkhaiojimnnjhhilmhjmhdbdagod?hl=en) and the 'Save' button will show up under each ad.

![swipekit extension get pageId of any ad inside the facebook ad library](https://swipekit.app/blog/articles/meta-ad-library-api/body-8.png)

Then press and hold Ctrl(or Command) and click on the save button and it will show the pageId on top of the Save button.

### Use a wrapper package to work with the API

I recommend this since working with the ad library is so crummy. I've created a [simple wrapper around the ad library here.](https://github.com/shash7/facebookadlibrary)

Since the API is ergonomically challenged, I highly recommend using this.

Installing the package.

You need nodejs to install the package. Run this inside your project:

npm install --save facebookadlibrary Then initiate the package like this:

import FacebookAdLibrary from "facebookadlibrary"; const facebookAdLibrary = new FacebookAdLibrary(token); Pass the token from your Facebook app you created earlier

### Examples

Find a specific page's ads:

const ads = await facebookAdLibrary.findByPageId(pageId); //Get the pageId from the technique I showed earlier

Find a specific ad's data:

As I said earlier, there's no way to find a specific ad's data. However you can find a page's ads and paginate them. While looping, just check if any record matches the adId and return it.

const ad = await facebookAdLibrary.findByAdId(adId, pageId); //You'll need to pass both the adId and pageId to get this ad

Note that this package caps returned ads at 500. If you absolutely want to find a specific ad, pass limit: -1 as a parameter.

const ad = await facebookAdLibrary.findByAdId(adId, pageId, { limit: -1 } );

Find ads by a search term

This is great for doing broad competitor research, finding winning products and more.

```
const searchTermAds = await facebookadlibrary.findBySearchTerm('skincare');
```

Passing search paramters

You can pass search params as defined by the [Facebook ad library API's docs.](https://www.facebook.com/ads/library/api/)

You can pass this paramter object as the last param in all functions exposed in the FacebookAdLibrary functions.

// Get all active ads only const activeAds = await facebookadlibrary.findBySearchTerm('skincare', {ad\_active\_status: 'ACTIVE' });

// Get ads within a certain time period(eg: 7th July, 2024 to 24 Feb 2025) const activeAds = await facebookadlibrary.findBySearchTerm('skincare', {ad\_delivery\_date\_min: '2024-07-07', ad\_delivery\_date\_max: '2025-02-24' });

// Get ads with a specific media type(options: ALL, IMAGE, MEME, VIDEO, NONE) const activeAds = await facebookadlibrary.findBySearchTerm('skincare', { media\_type: 'VIDEO' });

// Get ads with a specific language(s)(eg, Spanish). You need to pass a string that looks like an array. You can also JSON.stringify an array and pass it. const activeAds = await facebookadlibrary.findBySearchTerm('skincare', { languages: "\['es'\]" });

## Final thoughts

The Meta API is powerful but has its quirks. Be ready to handle pagination and work around some limitations like fetching specific ads directly.

Despite this, it’s an invaluable tool for marketers handling large-scale ad analysis.

---

## Common Questions

- ### Once I verify my Facebook developer account, is the verification tied to an app?
	No, the verification is a process.
	Once the process is complete, all your Facebook apps will be able to access the ad library API endpoints.
- ### Will the API expire?
	Yes it will expire in a short time.
	To make it's expiry longer(3 months), head over to the Graph API explorer tool and click on the "i" icon.
	Then click on the button in the popup and this will take you to another page.
	![Extend Facebook API token](https://dashboard.swipekit.app/assets/dc9591ac-4d46-4b30-ab99-28241c504743?width=1472&height=866)
	Here, click on the "Extend Access Token" button and this will generate a new access token there. Save this somewhere.
	---
	Ideally, you'd want to implement a refresh token mechanism where you can get a new token every now and then using cron jobs or something similar.
	However this is beyond the scope of this article.