#Events Page

**Goal:** The Hautelook events page serves to show customers whixh events are currently active, which events are ending soon, and which events are coming soon. It also serves promotional messages to customers in order to entice and encourage conversion.

**Design:** Wires, specs, and comps can all be found within the [Invision project](https://hautelook.invisionapp.com/d/main#/projects/prototypes/10271933)

##Table of Contents
* [Event Tiles](#event-tiles)
 * [Main Event Tile](#main-event-tile)
 * [Secondary Event Tiles](#secondary-event-tiles)
 * [Marketing Seals](#marketing-seals)
 * [Also New Today](#also-new-today)
 * [Events Ending Soon](#events-ending-soon)
 * [Upcoming Events](#upcoming-events)
* [Promotional Tiles](#promotional-tiles)
 * [Marketing Promo Banner](#marketing-promo-banner)
 * [Promo Carousel](#promo-carousel)
 * [Promo Grid Tile 1](#promo-grid-tile-1)
 * [Promo Grid Tile 2](#promo-grid-tile-2)
 * [Marketing Bottom Promo Banner](#marketing-bottom-promo-banner)
 


##Event Tiles

Events are pulled into the events page from the /v4/events API.

When customer lands on [www.hautelook.com](https://www.hautelook.com/) or [www.hautelook.com/events/all](https://www.hautelook.com/events/all):
* Events should be displayed in tiles based on sort order as returned by the Events API

When customer lands on www.hautelook.com/events/category_name:
* Events returned from the Events API should be filtered by the event category that is in the URL.
 * /events/women should filter events that have
```JSON
tab_category: "Women"
```
 * /events/men should filter events that have
```JSON
tab_category: "Men"
```
 * /events/kids should filter events that have
```JSON
tab_category: "Kids"
```
 * /events/home should filter events that have
```JSON
tab_category: "Home"
```
 * /events/beauty should filter events that have
```JSON
tab_category: "Beauty"
```
* Events filtered for the selected category should maintain sort order as returned by the Events API.

**Note:** The following is when there are no Promo CMS tiles scheduled. See [Promotional Tiles](#promotional-tiles) for direction on page layout when Promotional Tiles are scheduled.

[Back to Top](#events-page)


###Main Event Tile

The event returned with the highest priority should be displayed in the Main Event Hero Tile. See  [Events-Page-Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218557435_Events-Page-Wireframe) for placement.

#####Image file

Image is found in the API under

```JSON
_links: {
  http://hautelook.com/rels/images/event-hero: {
  href:"https://fastly.hautelookcdn.com/assets/event_name_folder/event-hero.jpg"
  },
}
```

When customer clicks on the Main Event Tile image, they should be taken to the URL that is returned in the API as

```JSON
self: {
href: "https://www.hautelook.com/api/events/event_id"
},
```

#####Hero Text and SHOP NOW CTA

See comps:
* [Main-Event-Hero-White](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218565745_Main-Event-Hero-Comp-White)
* [Main-Hero-Event-Black](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218565744_Main-Event-Hero-Comp-Black)

See specs:
* [Main-Event-Hero-Spec](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218566558_Main-Event-Hero-Spec)

If the API returns "text-blue" or "text-white", live headline text and SHOP NOW button should be displayed.

```JSON
display_format: "text-blue"
```

*or*

```JSON
display_format: "text-white"
```

**DISCOVERY NOTE**: It is unclear where the actual live headline text is pulled from as I do not see it in the API currently since all heroes presently have text burned in. Also unclear if the entire tile will then be clickable or only the SHOP NOW CTA.
  * Font = Source Sans Pro, Bold, pt size 37.5
  * **DISCOVERY:** Can Headline can display as black text?? In admin, only options for blue, white, no text
   * Assuming that "text-white" will lead to white headline and "text-blue" will lead to blue (#2f384e) headline.
  * Headline copy can wrap up to 4 lines of text. Each line should wrap at 330px.
  * Headline text + the CTA button should always be vertically center-aligned with the height of the image.

If the API returns "Regular", headline text and SHOP NOW button should not be displayed.

```JSON
display_format: "Regular"
```

[Back to Top](#events-page)

###Secondary Event Tiles


Events in sort order 2-30 should appear in 2x2 grid. See [Events-Page-Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218557435_Events-Page-Wireframee).

See comp:
* [Secondary-Event-Tiles-Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218569896_Secondary-Event-Tiles-Comp)

**NOTE**: Comp shows the Promo Carousel active. If Promo Carousel is not active then Secondary Tiles 1 and 2 should appear the same as Secondary Tiles 3 and 4.

#####Image file

Image file is found in the /events API as either

**NEEDS DISCOVERY**

```JSON
http://hautelook.com/rels/images/event-square: {
href:"https://fastly.hautelookcdn.com/assets/event_name_folder/event-square.jpg"
},
```
*or*

```JSON
http://hautelook.com/rels/images/event-main: {
href:"https://fastly.hautelookcdn.com/assets/event_name_folder/event-main.jpg"
},
```
When customer clicks on the Secondary Event Tile image, they should be taken to the URL that is returned in the API as

```JSON
self: {
href: "https://www.hautelook.com/api/events/eventID"
},
```

#####Event Title banner
 * The Event Title should be displayed as text in a banner overlay.
```JSON
title: "event_title"
```

 * Event Ends countdown banner should be displayed above the Event Title banner for all events ending in less than 24 hours as determined by
```JSON
end_date: "<date_time>",
```
 Banner text should show remaining time in whole Hours:
   * If the event ends in 24 hours, 4 minutes, no banner should display.
   * If the event ends in 23 hours, 59 minutes, banner should display "*Ends in 23 hours*"
   * If the event ends in 16 hours, 36 minutes, banner should display “*Ends in 16 hours*”
   * If the event ends in 1 hour, 59 minutes, banner should display “*Ends in 1 hour*”
   * If the event ends in 1 hour, 1 minute, banner should display “*Ends in 1 hour*”
   * If the event ends in 1 hour or less, the banner should read "*Ends in less than 1 hour*"

###Marketing Seals

Marketing seals are added in Hautelook admin to certain events. If a marketing seal has been added in admin, an additional graphic on the Event Tile is required.

Seals are sent via the Events API as

**NEEDS DISCOVERY**

```JSON
_links: {http://hautelook.com/rels/images/seals/event-hero: {
href: "https://www.hautelookcdn.com/images/scrims/seal_name_EventPage.png"
},
}
```
*or*
```JSON
_links: {http://hautelook.com/rels/images/seals/catalog-banner: {
href: "https://www.hautelookcdn.com/images/scrims/seal_name_CatalogBanner.png"
},
}
```
See comp - [Marketing Seal Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218814575_Marketing-Seal-Comp) for placement.

* The graphic should be positioned at the top righthand corner of the tile.
  * **NOTE**: seals are always assigned at the event level.
  * **NOTE**: Event Tiles in the Ending Soon section (on All and Women) do not support marketing seals.
  * **NOTE**: Event images displayed under Also New Today will never include event seals as well.

###Also New Today

The Also New Today section should appear below the Main and Secondary event tiles.

See comp - [Also New Today Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218821978_Also-New-Today-Comp)

**NOTE**: This section does not appear for /events/all

'Also New Today' should include four placements, one for each vertical that is NOT currently in view.

* Each placement should include a vertical banner, image, and “See All” text link.
 * Clickable vertical banner should be displayed above the corresponding event image.
   * Clicking banner should open the corresponding events vertical page.
 * The first/top sorted event image (by master sort order) by vertical should appear in each placement.
  * Placement should not include the Event Title banner.
 * A "See All" text link should be displayed below the corresponding event image.
   * Clicking “See All” should open the event page to the corresponding event vertical.


###Events Ending Soon

The Events Ending Soon section should appear below the Main and Secondary event tiles. If an 'Also New Today' section is present, 'Events Ending Soon' should appear below.

**NOTE**: This section SHOULD NOT appear for /events/men, /events/kids, /events/home, or /events/beauty.

See Comps and Specs:
* [Events-Ending-Soon-Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218819562_Events-Ending-Soon-Comp)
* [Events-Ending-Soon-Spec](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218819976_Events-Ending-Soon-Spec)

The first row should display 2 event tiles across. Remaining events display 3 tiles across each row. All grid images can be found in the Events API under:

```JSON
http://hautelook.com/rels/images/event-main: {
href:"https://fastly.hautelookcdn.com/assets/event_name_folder/event-main.jpg"
},
```

**NOTE**: The images for Events Ending Soon will need to be resized to fit the layout.

###Upcoming Events

The Upcoming Events should be displayed below the Events Ending Soon section. The section should display upcoming events grouped by day/date in three columns.

See Comp - [Upcoming-Events-Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218823484_Upcoming-Events-Comp)


Upcoming events can be found using the /events/upcoming API.  The section should be dynamically populated based on the event vertical currently in view.

i.e. if current URL is /events/women, Upcoming Events section should show the upcoming events with

```JSON
tab_category: "Women"
```
**NOTE**: If the Home vertical is selected, do not display the Upcoming Events section.

##Promotion Tiles

Promotional tiles are scheduled in Hautelook admin [Promo CMS](https://admin.hautelook.net/promo-cms/schedule) and affect the positions and sizes of Event Tiles. Promotional tiles are returned via the /promotions API.

###Marketing Promo Banner

The Marketing Promo banner is returned from the /promotions API as  

```JSON
promo_placement: "ember_top_promo"
```

If a Marketing Promo Banner is returned as

```JSON
active: "true"
```

it should appear below the header navigation. See [Promotional Tiles - ember_top_promo Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218815514_Promotional_Tiles_-_Ember_Top_Promo_Wireframe) for placement.

**DISCOVERY NOTE**: It appears that the image and the destination URL (if included) are included in the Promotions API under:

```JSON
promo_resource: "",
```

* Asset will always extend the 960px wide but can vary in height. Asset provided as an image and will never include live text.
 * **NOTE**: I believe we redefined the width from 962px to 960px when implementing on the new NR homepage.
  * If a link is scheduled for the placement, the entire asset should be clickable.
  * If a link has not be scheduled, just display the image.
* Promo banners can be targeted to display on specific event verticals (All Events, Women, Men, Kids, Home, and/or Beauty) using

```JSON
event_tab: "vertical_name"
```

###Promo Carousel

The  Promo Carousel is returned from the /promotions API as  

```JSON
promo_placement: "ember_rotating_promo"
```

If a  Promo Carousel is

```JSON
active: "true"
```

it should appear after the Event Secondary Tile 2.

**DISCOVERY NOTE**: It appears that the image and the destination URL are included in the Promotions API under:

```JSON
promo_resource: "",
```

**NOTE**: When a Promo Carousel is live, the Event Secondary Tile 2 will no longer follow the 2x2 grid pattern.

See [Promotional Tiles - ember_rotating_promo Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218815685_Promotional_Tiles_-_Ember_Rotating_Promo_WireframeK) for placement.

**DISCOVERY NOTE**: I am not sure how the image is resized, or which image is called for the event in Secondary Tile 2 when the Promo Carousel is scheduled.

* Promo carousel content should be served based on user's gender selected.
 * If gender is not set (logged out),  the promo carousel should default to Female.
* It may have 1, 2 or 3 options for its rotation slot.
 * If 2 or 3 promo units are scheduled, carousel should auto-rotate for 3 cycles.
 * If 2 or 3 promo units are scheduled, carousel dots should be displayed at the bottom of placement to navigation between promo units.
   * Style dots to indicate promo unit currently in view.
   * On-click of carousel dot, carousel should move to corresponding promo unit.



###Promo Grid Tile 1

The  Promo Grid Tile 1 is returned from the /promotions API as  

```JSON
promo_placement: "ember_grid_promo_1"
```

If a Promo Grid Tile 1 is

```JSON
active: "true"
```

it should be displayed as the same size as a Secondary Tile and should appear after Secondary Tile 5, pushing Secondary Tile 6. See [Promotional Tiles - ember_grid_promo_1 Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218816886_Promotional_Tiles_-_Ember_Grid_Promo_1_Wireframe) for placement.

**DISCOVERY NOTE**: It appears that the image and the destination URL are included in the Promotions API under:

```JSON
promo_resource: "",
```

**NOTE**: If 5 or less events are live, display after the last event.

###Promo Grid Tile 2

The  Promo Grid Tile 2 is returned from the /promotions API as  

```JSON
promo_placement: "ember_grid_promo_2"
```

If a Promo Grid Tile 2 is

```JSON
active: "true"
```

it should be displayed as the same size as a Secondary Tile and should appear after Secondary Tile 7, pushing Secondary Tile 6. See [Promotional Tiles - ember_grid_promo_2 Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218817757_Promotional_Tiles_-_Ember_Grid_Promo_2_Wireframe) for placement.


**NOTE**: If 6 or less events are live, display after the last event.

###Marketing Bottom Promo Banner

The Marketing Bottom Promo Banner is returned from the /promotions API as  

```JSON
promo_placement: "ember_bottom_promo"
```

If a Marketing Bottom Promo Banner is

```JSON
active: "true"
```

it should be displayed below the Upcoming Events section. See [Promotional Tiles - ember_bottom_promo Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218824372_Promotional_Tiles_-_Ember_Bottom_Promo_Wireframe) for placement.

**DISCOVERY NOTE**: It appears that the image and the destination URL are included in the Promotions API under:

```JSON
promo_resource: "",
```

This banner should not have a restriction on height and should go full-width across the page.
