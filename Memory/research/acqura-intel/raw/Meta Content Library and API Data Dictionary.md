<iframe frameborder="0" height="0" width="0" src="https://developers.facebook.com/common/referer_frame.php?cb=1"></iframe><iframe frameborder="0" height="0" width="0" src="https://developers.facebook.com/common/referer_frame.php?cb=1"></iframe><iframe frameborder="0" height="0" width="0" src="https://developers.facebook.com/common/referer_frame.php?cb=1"></iframe><iframe frameborder="0" height="0" width="0" src="https://developers.facebook.com/common/referer_frame.php?cb=1"></iframe>

## Data dictionary

This data dictionary describes the data names displayed in the Meta Content Library web UI (the Name column) if applicable, and the corresponding API fields returned in Meta Content Library API search responses (the API field column). In the API field column, some fields have nested fields indicated by a dot notation. These are referred to as *expanded fields*. See [Field expansion](https://developers.facebook.com/docs/content-library-api/field-expansion) for information about how to include some or all of a parent field's expanded fields in your queries.

## Scope of data included in Meta Content Library and API

### Facebook

#### Public content dataset

Posts to the following:

- Pages, groups and events
- Profiles with 100 or more followers
- Profiles that are [verified](https://www.facebook.com/help/196050490547892)

Meta Content Library surfaces posts by original producers only (excludes collaborators).

#### Downloadable subset

Posts to the above surfaces from the following:

- Pages with 15,000 or more likes or followers
- Profiles with 100 or more followers
- Profiles that are [verified](https://www.facebook.com/help/196050490547892)

### Facebook Marketplace

#### Public content dataset

Public listings on Facebook Marketplace from Pages or profiles, excluding the following:

- Listings marked as sold more than 1 month ago.
- Listings that have not been updated in the last 6 months.
- Listings with a privacy setting enabled, such as hiding a listing from friends.
- Job listings in some locations. See [About jobs on Facebook](https://www.facebook.com/help/2203257093390031) for more information.

### Facebook fundraisers

#### Public content dataset

- Public fundraisers on Facebook
- Fundraisers attached to public posts
- Reshares of public fundraisers (available in the posts data subset)

### Facebook channels

#### Public content dataset:

- Active channels with audience set to “anyone” or “followers” as long as the creator of the channel meets the criteria for inclusion in the Facebook public content dataset.
- All channel messages within public channels.

### Instagram

#### Public content dataset

Posts from the following:

- Business and creator accounts
- Personal accounts with 100 or more followers
- Personal accounts that are [verified](https://l.facebook.com/l.php?u=https%3A%2F%2Fhelp.instagram.com%2F733907830039577%3Fhelpref%3Dfaq_content&h=AT5595RG7ci50EUlylrcTw7Tmn4uZgQ_6ISw5YJJDRN4qxLtB98sZ_Gbe43gBHfcHvrfTETcbKkvBD8WRNF6xJeLEIPjffArvBltI69ykA7V_H48c-SDkNMHBDTh4xkJKlWQ5d3oCnjhOeR9G3TroshdwQ2rNd0_x72dAPbMuTg)

#### Downloadable subset

Posts from the following:

- Business and creator accounts with 100 or more followers
- Personal accounts with 100 or more followers
- Business, creator and personal accounts that are [verified](https://l.facebook.com/l.php?u=https%3A%2F%2Fhelp.instagram.com%2F733907830039577%3Fhelpref%3Dfaq_content&h=AT4oPsIOwyFb5EGsJQx1dSVSTc8VGGb3OhtUedOS-Sa5Z7MWkeC3aYiaP0GGVRot7WpzkTI4t_dmd61qQvk2BAMGWVPsDQLLdkAGjdWAWtWaC7WIGqJWn3GWyo6gx9n4h1Duuoq0ZMZ8GuFZTlVHPyprDGnUHhh0yt9GPHp1UcI)

Meta Content Library surfaces posts by original producers only (excludes collaborators).

### Instagram fundraisers

#### Public content dataset:

- Fundraisers created by public Instagram accounts
- Reshares of fundraisers (available in the posts data subset)

### Instagram channels

#### Public content dataset:

- Active channels with audience set to “anyone” or “followers” as long as the creator of the channel meets the criteria for inclusion in the Instagram public content dataset.
- All channel messages within public channels.

### Threads

#### Public content dataset:

- Posts shared by public profiles with 100 or more followers

**Note**: Threads content is not available for download while this dataset is in development as data quality may have significant variation.

**Facebook Page**

| Name | API field | Description | Products |
| --- | --- | --- | --- |
| Meta Content Library ID | id | Unique ID linked to a Facebook Page; cannot be used to search on Meta technologies. | Content Library API |
| Name | name | The name of the Facebook Page. | Content Library  Content Library API |
| Username | username | The username of the Facebook Page, if available. | Content Library API |
| About | about | The short paragraph from the Facebook Page About section. | Content Library  Content Library API |
| Website | website | The external URL from the Facebook Page About section. | Content Library API |
| Description | description | The long paragraph from the Facebook Page About section. | Content Library  Content Library API |
| Verification status | verification\_status | The verification status of the Facebook Page. [Learn more about verified Pages and profiles.](https://www.facebook.com/help/196050490547892) | Content Library  Content Library API |
| Page categories | page\_categories | The list of up to three categories of the Facebook Page, selected by the Page manager. | Content Library  Content Library API |
| Location city | location.city | The self-reported, publicly accessible city location associated with the Facebook Page. | Content Library API |
| Location country | location.country | The self-reported, publicly accessible country location associated with the Facebook Page. | Content Library API |
| Location country code | location.country\_code | The self-reported, publicly accessible country code location associated with the Facebook Page. | Content Library API |
| Location name | location.name | The self-reported, publicly accessible location name associated with the Facebook Page. | Content Library API |
| Location region | location.region | The self-reported, publicly accessible region location associated with the Facebook Page. | Content Library API |
| Location zip | location.zip | The self-reported, publicly accessible location zip associated with the Facebook Page. | Content Library API |
| Location street | location.street | The self-reported, publicly accessible street location associated with the Facebook Page. | Content Library API |
| Location state | location.state | The self-reported, publicly accessible state location associated with the Facebook Page. | Content Library API |
| Page name change date | page\_transparency.page\_name\_changes.data.date | The date of Facebook Page name change. | Content Library API |
| Page name old | page\_transparency.page\_name\_changes.data.old\_name | The old name of the Facebook Page prior to the name change. | Content Library API |
| Page name new | page\_transparency.page\_name\_changes.data.new\_name | The new name of the Facebook Page, following the name change. | Content Library API |
| Page merged date | page\_transparency.page\_merges.data.date | The date another Facebook Page merged with this Page. | Content Library API |
| Page merged | page\_transparency.page\_merges.data.page\_merged | The name of the Facebook Page that merged with this Page. | Content Library API |
| Creation date | creation\_date | The date the Facebook Page was created. | Content Library  Content Library API |
| Page manager countries | page\_transparency.admin\_countries.data.country | The predicted primary country locations of people who manage this Facebook Page. See [What location information does Meta receive?](https://www.facebook.com/privacy/dialog/what-location-information-does-meta-receive) for more information. | Content Library  Content Library API |
| Count of Page managers by countries | page\_transparency.admin\_countries.data.count | The number of people who manage this Facebook Page predicted to be from the associated country. | Content Library  Content Library API |
| Page owner | page\_transparency.confirmed\_page\_owner | The confirmed owner associated with the Facebook Page. | Content Library API |
| Has active ads | page\_transparency.has\_active\_ads | Whether the Facebook Page has active ads or not. | Content Library API |
| Has run political ads | page\_transparency.has\_run\_political\_ads | Whether the Facebook Page has run political ads or not. | Content Library API |
| Followers | follower\_count | The number of followers of the Facebook Page. | Content Library  Content Library API |
| Page likes | like\_count | The number of likes of the Facebook Page. | Content Library API |

**Facebook group**

| Name | API field | Description | Products |
| --- | --- | --- | --- |
| Meta Content Library ID | id | Unique ID linked to a Facebook group; cannot be used to search on Meta technologies. | Content Library API |
| Name | name | The name of the Facebook group. | Content Library  Content Library API |
| Username | username | The username (group name identifier) of the Facebook group, if available. | Content Library API |
| Description | description | The description of the Facebook group. | Content Library  Content Library API |
| Creation date | creation\_date | The date the Facebook group was created. | Content Library  Content Library API |
| Group original name | group\_transparency.original\_name | The original name of the Facebook group. | Content Library API |
| Group name change date | group\_transparency.name\_changes.data.date | The date the name of the Facebook group changed. | Content Library  Content Library API |
| Group name new | group\_transparency.name\_changes.data.new\_name | The new name of the Facebook group. | Content Library API |
| Group admin and moderator Page Meta Content Library IDs | group\_transparency.admin\_and\_moderator\_page\_ids | The list of Unique IDs linked to the Facebook Pages that are admins or moderators of the Facebook group. These unique IDs cannot be used to search on Meta technologies. | Content Library API |
| Group owner type | group\_owners.data.type | The type of the group owner associated with the Facebook group.This field will display if the group owner is a professional profile or Page. | Content Library API |
| Group owner Meta Content Library ID | group\_owners.data.id | Unique ID of the Facebook group owners. This field will display if the group owner is a professional profile or Page. | Content Library API |
| Picture URL | picture\_url | The photo URL of the Facebook group. | Content Library API |
| Group members | member\_count | The number of members of the Facebook group. | Content Library  Content Library API |

**Facebook event**

| Name | API field | Description | Products |
| --- | --- | --- | --- |
| Meta Content Library ID | id | Unique ID linked to a Facebook event; cannot be used to search on Meta technologies. | Content Library API |
| Name | name | The name of the Facebook event. | Content Library  Content Library API |
| Description | description | The description of the Facebook event. | Content Library  Content Library API |
| Creation time | creation\_time | The time the Facebook event was created. | Content Library API |
| Event start time | event\_start\_time | The start time of the Facebook event. Not available if the event is the parent of recurring event instances. [Learn more about recurring events](https://developers.facebook.com/docs/content-library-api/guide-fb-events#recurring). | Content Library  Content Library API |
| Event end time | event\_end\_time | The end time of the Facebook event. Not available if the event is the parent of recurring event instances. [Learn more about recurring events](https://developers.facebook.com/docs/content-library-api/guide-fb-events#recurring). | Content Library API |
| Going responses | going\_count | The number of Going responses on a Facebook event. Not available if the event is the parent of recurring event instances. [Learn more about recurring events](https://developers.facebook.com/docs/content-library-api/guide-fb-events#recurring). | Content Library  Content Library API |
| Interested responses | interested\_count | The number of Interested responses on a Facebook event. Not available if the event is the parent of recurring event instances. [Learn more about recurring events](https://developers.facebook.com/docs/content-library-api/guide-fb-events#recurring). | Content Library  Content Library API |
| Event type | event\_type | The type of Facebook event. Event types include single instance, recurring or instance of recurring. | Content Library API |
| Recurring event Meta Content Library IDs | recurring\_event\_ids | The list of unique Meta Content Library IDs of the recurring instances of the Facebook event, if the event is recurring; these unique IDs cannot be used to search on Meta technologies. Only available if the event is the parent of recurring event instances. [Learn more about recurring events](https://developers.facebook.com/docs/content-library-api/guide-fb-events#recurring). | Content Library API |
| Parent event ID | parent\_event\_id | The unique ID of the parent event of the Facebook event, if the event is recurring; cannot be used to search on Meta technologies. Only available if the event is an instance of a recurring event. [Learn more about recurring events](https://developers.facebook.com/docs/content-library-api/guide-fb-events#recurring). | Content Library API |
| Event owners type | event\_owners.data.type | The type of the event owner associated with the Facebook event. | Content Library API |
| Event owners Meta Content Library ID | event\_owners.data.id | The unique ID of the event owner associated with the Facebook event; cannot be used to search on Meta technologies. This field will display if the event owner is a group, professional profile or Page. For events owned by professional profiles or Pages, only the Meta Content Library Page ID will be shared. | Content Library API |
| Place name | place.name | The self-reported, publicly accessible name of the place where the Facebook event is located. | Content Library API |
| Place location city | place.location.city | The self-reported, publicly accessible city where the Facebook event is located. | Content Library API |
| Place location country | place.location.country | The self-reported, publicly accessible country where the Facebook event is located. | Content Library API |
| Place location country code | place.location.country\_code | The self-reported, publicly accessible country code of the Facebook event’s location. | Content Library API |
| Place location name | place.location.name | The self-reported, publicly accessible name of the Facebook event’s location. | Content Library API |
| Place location region | place.location.region | The self-reported, publicly accessible region where the Facebook event is located. | Content Library API |
| Place location state | place.location.state | The self-reported, publicly accessible state where the Facebook event is located. | Content Library API |
| Place location street | place.location.street | The self-reported, publicly accessible street where the Facebook event is located. | Content Library API |
| Place location zip | place.location.zip | The self-reported, publicly accessible zip of the Facebook event’s location. | Content Library API |

**Facebook profile**

| Name | API field | Description | Products |
| --- | --- | --- | --- |
| Meta Content Library ID | id | Unique ID linked to a Facebook profile; cannot be used to search on Meta technologies. | Content Library API |
| Name | name | The name of the Facebook profile, if the user meets [eligibility criteria](#available-public-data). | Content Library Content Library API |
| Username | username | The username of the Facebook profile, if available and profile meets [eligibility criteria](#available-public-data). | Content Library API |
| About | about | Text of the 'About' section. | Content Library Content Library API |
| Follower count | follower\_count | The number of followers of the Facebook profile. | Content Library Content Library API |
| Intro | intro | Text of intro. | Content Library Content Library API |
| Verification status | verification\_status | Verification status. Possible values: not\_verified and blue\_verified. | Content Library Content Library API |
| Creation date | creation\_date | The date the Facebook profile was created. | Content Library Content Library API |
| Profile categories | profile\_categories | The list of up to three categories of the Facebook profile, selected by the profile owner. | Content Library Content Library API |
| Admin countries | profile\_transparency.admin\_countries | List of predicted primary country locations of the Facebook profile owner. See [What location information does Meta receive?](https://www.facebook.com/privacy/dialog/what-location-information-does-meta-receive) for more information. | Content Library Content Library API |
| Has active ads | profile\_transparency.has\_active\_ads | Whether the Facebook profile has active ads or not. | Content Library Content Library API |
| Picture height | picture.height | Height of the photo URL of the Facebook profile. | Content Library Content Library API |
| Picture URL | picture.url | The photo URL of the Facebook profile. | Content Library Content Library API |
| Picture width | picture.width | Width of the photo URL of the Facebook profile. | Content Library Content Library API |
| Websites | websites | The external URLs from the Facebook profile’s 'About' section. | Content Library Content Library API |

**Facebook post**

| Name | API field | Description | Products |
| --- | --- | --- | --- |
| Meta Content Library ID | id | Unique ID linked to a Facebook post; cannot be used to search on Meta technologies. | Content Library  Content Library API |
| Text | text | The text of the Facebook post. Tags are excluded. Not applicable to stories. | Content Library  Content Library API |
| Match type | match\_type | List of match types for text searches in text, images and stories. Match types include:  - `post_text` for posts that match based on text in text-only posts - `image_text` for posts that match based on text-in-image posts - `multimedia_text` for story highlights that match based on text search | Content Library  Content Library API |
| Activity type | activities.type | Type of activity represented in a post. Activity types include `streaming` and `playing` (of a gaming video). | Content Library  Content Library API |
| Is verified | is\_verified | Whether the post was made from a Facebook surface that is verified (only Pages and profiles can be verified). | Content Library  Content Library API |
| Activity name | activities.name | Name of the activity represented in a post. For example, if the activity type is `streaming` or `playing` (of a gaming video), this would be the name of the game being played. | Content Library  Content Library API |
| Creation time | creation\_time | The time the Facebook post was created. | Content Library  Content Library API |
| Modified time | modified\_time | The time the Facebook post was most recently modified. | Content Library API |
| Language | lang | The content language of the Facebook post. Returns ISO 639-1 language code in 2-letter lowercase format. | Content Library (Filter only)  Content Library API |
| Likes | statistics.like\_count | The number of like reactions on the post. Not applicable to stories. | Content Library  Content Library API |
| Love reactions | statistics.love\_count | The number of love reactions on the post. Not applicable to stories. | Content Library  Content Library API |
| Wow reactions | statistics.wow\_count | The number of wow reactions on the post. Not applicable to stories. | Content Library  Content Library API |
| Haha reactions | statistics.haha\_count | The number of haha reactions on the post. Not applicable to stories. | Content Library  Content Library API |
| Sad reactions | statistics.sad\_count | The number of sad reactions on the post. Not applicable to stories. | Content Library  Content Library API |
| Angry reactions | statistics.angry\_count | The number of angry reactions on the post. Not applicable to stories. | Content Library  Content Library API |