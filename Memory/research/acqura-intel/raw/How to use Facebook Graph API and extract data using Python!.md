Hi all,

This is my second story on Medium.com. I have moved on from struggling to code to being a bit comfortable since the [first story](https://medium.com/@raviranjan_64687/big-data-insertion-into-neo4j-a-non-coders-tale-c3bcf5ef7f2a#.omnfkcycs). I wrote a Python code to extract publicly available data on Facebook. Let’s dive into it.

**Getting the Access Token:**

To be able to extract data from Facebook using a python code you need to register as a developer on Facebook and then have an access token. Here are the steps for it.

1. Go to link [developers.facebook.com](http://developers.facebook.com/), create an account there.
2. Go to link [developers.facebook.com/tools/explorer](https://developers.facebook.com/tools/explorer).
3. Go to “My apps” drop down in the top right corner and select “add a new app”. Choose a display name and a category and then “Create App ID”.
4. Again get back to the same link [developers.facebook.com/tools/explorer](https://developers.facebook.com/tools/explorer). You will see “Graph API Explorer” below “My Apps” in the top right corner. From “Graph API Explorer” drop down, select your app.
5. Then, select “Get Token”. From this drop down, select “Get User Access Token”. Select permissions from the menu that appears and then select “Get Access Token.”
6. Go to link [developers.facebook.com/tools/accesstoken](https://developers.facebook.com/tools/accesstoken/). Select “Debug” corresponding to “User Token”. Go to “Extend Token Access”. This will ensure that your token does not expire every two hours.

**Python Code to Access Facebook Public Data:**

Go to link [https://developers.facebook.com/docs/graph-api](https://developers.facebook.com/docs/graph-api) if want to collect data on anything that is available publicly. See [https://developers.facebook.com/docs/graph-api/reference/v2.7/](https://developers.facebook.com/docs/graph-api/reference/v2.7/). From this documentation, choose any field you want from which you want to extract data such as “groups” or “pages” etc. Go to examples of codes after having selected these and then select “facebook graph api” and you will get hints on how to extract information. This blog is primarily on getting events data.

First of all, import ‘urllib3’, ‘facebook’, ‘requests’ if they are already available. If not, download these libraries. Define a variable token and set its value to what you got above as “User Access Token”.

```c
token= ‘aiufniqaefncqiuhfencioaeusKJBNfljabicnlkjshniuwnscslkjjndfi’
```

**Getting list of Events:**

Now to find information on events for any search term say “Poetry” and limiting those events’ number to 10000:

```c
graph = facebook.GraphAPI(access_token=token, version = 2.7)
events = graph.request(‘/search?q=Poetry&type=event&limit=10000’)
```

This will give a dictionary of all the events that have been created on Facebook and has string “Poetry” in its name. To get the list of events, do:

```c
eventList = events[‘data’]
```

**Extracting all information for a event from the list of events extracted above:**

## Get Ravi Ranjan’s stories in your inbox

Join Medium for free to get updates from this writer.

Get the EventID of the first event in the list by

```c
eventid = eventList[1][‘id’]
```

For this EventID, get all information and set few variables which will be used later by:

```c
event1 = graph.get_object(id=eventid,
 fields=’attending_count,can_guests_invite,category,cover,declined_count,description,end_time,guest_list_enabled,interested_count,is_canceled,is_page_owned,is_viewer_admin,maybe_count,noreply_count,owner,parent_group,place,ticket_uri,timezone,type,updated_time’)
attenderscount = event1[‘attending_count’]
declinerscount = event1[‘declined_count’]
interestedcount = event1[‘interested_count’]
maybecount = event1[‘maybe_count’]
noreplycount = event1[‘noreply_count’]
```

Getting the list of all those who are attending an event and converting the response into json format:

```c
attenders = requests.get(“https://graph.facebook.com/v2.7/"+eventid+"/attending?access_token="+token+”&limit=”+str(attenderscount)) attenders_json = attenders.json()
```

Getting the admins of the event:

```c
admins = requests.get(“https://graph.facebook.com/v2.7/"+eventid+"/admins?access_token="+token)admins_json = admins.json()
```

And similarly you can extract other information such as photos/videos/feed of that event if you want.

Go to [https://developers.facebook.com/docs/graph-api/reference/event/](https://developers.facebook.com/docs/graph-api/reference/event/) and see “Edges” part in the documentation. See image

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*h6JmVmvoJU0mPpBEE2_4vg.png)

Now, let’s say, you want to have a list of all those who are interested in the event, click on ‘interested’ green word here. This will open up a new page:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*sYrPBl2NAF3ZMxkfaMLfsA.png)

Select ‘Graph API Explorer’ here. This will open a new page:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*6gK5H0EMscabu36iyyNnJg.png)

Here, in place of {event-id}, put the id of the event, like this:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*w75PB19XpWLPiPe_pSuF2w.png)

Hit submit. Also, on the same page, you will find below ‘get code’ option

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*VoiBMqv5PxtLPKsCIzfcQw.png)

Select it to see the code. Select ‘curl’ in the pop up that appears and then get the same output in the python code, write it with requests.get as it has been shown in above examples.

Hope this helps those who are beginning to work with facebook graph API. I will be happy to hear your suggestions/questions/feedback.

If you found this blog of any value to you and if you are into cryptocurrencies and if you are generous, consider sending some ripples to the following address:

Destination Tag: 5973413

Wallet Address: rLdinLq5CJood9wdjY9ZCdgycK8KGevkUj

There are too many ifs in the above statement. Send only if all the three are true! Cryptocurrencies FTW!