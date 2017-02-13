#Events Page

**Goal:** The Hautelook events page serves to display to customers what events are currently active, which events are ending soon, andwhat events are coming soon. It also serves promotional messaging to customers in order to entice and encourage conversion.

**Design:** Wires, specs, and comps can all be found within the [Invision project](https://hautelook.invisionapp.com/d/main#/projects/prototypes/10271933)


##Event Tiles

Events are pulled into the events page from the /v4/events API.

When customer lands on [www.hautelook.com](https://www.hautelook.com/) or [www.hautelook.com/events/all](https://www.hautelook.com/):
* Events should be displayed in tiles based on sort order as returned by the Events API

When customer lands on [www.hautelook.com/events/<category_id>](https://www.hautelook.com/events/women):
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


###Main Event Tile

The event returned with the highest priority should be displayed in the Main Event Hero Tile position as seen in [Events-Page-Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218557435_Events-Page-Wireframe).

#####Image file is found in the API under

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

######If the API returns "text-blue" or "text-white" display live headline text and SHOP NOW button.

```JSON
display_format: "text-blue"
```

*or*

```JSON
display_format: "text-white"
```

**DISCOVERY NOTE**: It is unclear where the actual live headline text is pulled from as I do not see it in the API currently since all heroes presently have text burned in. Also unclear if the entire tile will then be clickable or only the SHOP NOW CTA.
  * Font = Source Sans Pro, Bold, pt size 37.5
  * **DISCOVERY:** Headline can display as black, white, or blue (#2f384e) text?? In admin, only options for blue, white, no text
   * Assuming that "text-white" will lead to white headline and "text-blue" will lead to blue (#2f384e) headline.
  * Headline copy can wrap up to 4 lines of. Each line will wrap at 330px.
  * Headline text + the CTA button is always vertically center-aligned with the height of the image.

######If the API returns "Regular", headline text and SHOP NOW button should not be shown.

```JSON
display_format: "Regular"
```

###Secondary Event Tiles


Events in sort order 2-30 should appear in 2x2 grid. See [Events-Page-Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218557435_Events-Page-Wireframee).

See comp:
* [Secondary-Event-Tiles-Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218569896_Secondary-Event-Tiles-Comp)

**NOTE**: Comp shows the Promo Carousel active. If Promo Carousel is not active then Secondary Tiles 1 and 2 would appear the same as Secondary Tiles 3 and 4 as in the Wireframe.

#####Image file found in the /events API as either

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
 * Display Event Title as text in banner overlay.
 ```JSON
title: "<event_title>"
 ```
 * Event Ends countdown banner should be displayed above the Event Title banner for all events ending in less than 24 hours as determined by
```JSON
end_date: "<date_time>",
```
 Banner text should show remaining time in whole Hours:
   * If the event ends in 24 hours, 4 minutes, do not display additional banner.
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
See comp - [Marketing Seal Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218814575_Marketing-Seal-Comp)

* Position the graphic at the top righthand corner of the tile.
  * **NOTE**: seals are always assigned at the event level.
  * **NOTE**: Event Tiles in the Ending Soon section (on All and Women) do not support marketing seals.
  * **NOTE**: Event images displayed under Also New Today will never include event seals as well.

###Also New Today

This section should appear below the Main and Secondary event tiles.

See comp - [Also New Today Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218821978_Also-New-Today-Comp)

**NOTE**: This section does not appear for /events/all

'Also New Today' includes four placements, one for each vertical that is NOT currently in view.

* Each placement includes a vertical banner, image, and “See All” text link.
 * Display clickable vertical banner above the corresponding event image.
   * Clicking banner opens the corresponding events vertical page.
 * Display the first/top sorted event image (by master sort order) by vertical in each placement.
   * NOTE: placement does not include the Event Title banner, only the image.
 * Display a "See All" text link below the corresponding event image.
   * Clicking “See All” opens the event page to the corresponding event vertical.


###Events Ending Soon

This section should appear below the Main and Secondary event tiles. If an 'Also New Today' section is present, 'Events Ending Soon' should appear below.

**NOTE**: This section SHOULD NOT appear for /events/men, /events/kids, /events/home, or /events/beauty.

See Comps and Specs:
* [Events-Ending-Soon-Comp](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218819562_Events-Ending-Soon-Comp)
* [Events-Ending-Soon-Spec](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218819976_Events-Ending-Soon-Spec)


###Upcoming Events

Upcoming should be displayed at the bottom of the page. The section should display upcoming events grouped by day/date in three columns.

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

* Asset will always extend the 960px wide but can vary in height.
  * **NOTE**: asset provided as an image and will never include live text.
 * **NOTE**: I believe we redefined the width from 962px to 960px when implementing on the new NR homepage.
* Destination link can be scheduled via admin and returned via promotions API:
  * If a link is scheduled for the placement, the entire asset should be clickable.
  * If a link has not be scheduled, just display the image.
* Promo banners can be targeted to display on specific event verticals (All Events, Women, Men, Kids, Home, and/or Beauty) using event_tab.

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

**NOTE**: When a Promo Carousel is live, the Event Secondary Tile 2 will no longer follow the 2x2 grid pattern.

See [Promotional Tiles - ember_rotating_promo Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218815685_Promotional_Tiles_-_Ember_Rotating_Promo_WireframeK) for placement.
* Promo carousel content is served based on user's gender selected.
 * If gender is not set (logged out), default the promo carousel to Female.
* It may have 1, 2 or 3 options for its rotation slot.
 * If 2 or 3 promo units are scheduled, auto-rotate for 3 cycles.
 * If 2 or 3 promo units are scheduled, display carousel dots at the bottom of placement to navigation between promo units.
   * Style dots to indicate promo unit currently in view.
   * On-click of carousel dot, jump to corresponding promo unit.
If no rotating promo unit is scheduled, the row instead displays Event tile 2 and 3.
Secondary Event tile uses event_main.jpg rather than event_medium.jpg in this scenario.


###Promo Grid Tile 1

The  Promo Grid Tile 1 is returned from the /promotions API as  

```JSON
promo_placement: "ember_grid_promo_1"
```

If a  Promo Carousel is

```JSON
active: "true"
```

it should be displayed as the same size as a Secondary Tile and should appear after Secondary Tile 5, pushing Secondary Tile 6. See [Promotional Tiles - ember_grid_promo_1 Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218816886_Promotional_Tiles_-_Ember_Grid_Promo_1_Wireframe) for placement.

**NOTE**: If 5 or less events are live, display after the last event.

###Promo Grid Tile 2

The  Promo Grid Tile 2 is returned from the /promotions API as  

```JSON
promo_placement: "ember_grid_promo_2"
```

If a  Promo Carousel is

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

If a  Promo Carousel is

```JSON
active: "true"
```

it should be displayed below the Upcoming Events section. See [Promotional Tiles - ember_bottom_promo Wireframe](https://hautelook.invisionapp.com/share/4ZAEWR22X#/218824372_Promotional_Tiles_-_Ember_Bottom_Promo_Wireframe) for placement.

This banner should not have a restriction on height and should go full-width across the page.
