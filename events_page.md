#Events Page

**Goal:** The Hautelook events page serves to display to customers what events are currently active, which events are ending soon, what events are coming soon. It also serves promotional messaging to customers in order to entice and encourage conversion.

**Design:** Wires, specs, and comps can all be found within the Invision project


##Event Tiles

Events are pulled into the events page from the /v4/events API. The following information is provided in the API:
* Event information
* Event Category
* Event Sort order

When customer lands on [www.hautelook.com](https://www.hautelook.com/) or [www.hautelook.com/events/all](https://www.hautelook.com/):
* Events should be displayed in tiles based on predetermined sort order as returned by the /v4/events API

When customer lands on [www.hautelook.com/events/CATEGORY](https://www.hautelook.com/events/women):
* Events returned from the /v4/events API should be filtered by the event category that is in the URL.
* Events filtered for the selected category should maintain relative sort order as returned by the /v4/events API.

**Note:** The following is when there are no Promo CMS tiles scheduled. See [Promotional Tiles](#promotional-tiles)


###Main Event Tile

The event returned with the highest priority should be displayed in the Main Event Hero Tile position as seen in [Events Page](ADD INVISION LINK).
* If the Event Hero is set to “display live text”, display live headline text and SHOP NOW button.
 * Font = Source Sans Pro, Bold, pt size 37.5
 * There is a db setting to determine the font color.
   * Headline can display as black, white, or blue (#2f384e) text.
 * Headline copy can wrap up to 4 lines of. Each line will wrap at 330px.
 * Headline text + the CTA button is always vertically center-aligned with the height of the image.
* If the Event hero is set to “not display live text”, do not display headline copy OR the SHOP NOW button.
* Image file = event-hero.jpg

###Secondary Event Tiles


Events in sort order 2-30 should appear in 2x2 grid.

* Event Image
 * event-main.jpg
* Event Title banner
 * Display Event name as text in banner overlay.
   * See spec.
* Event Ends countdown banner
 * Display additional banner above the Event Title banner for all events ending in less than 24 hours.
 * Banner text should show remaining time in whole Hours:
   * If the event ends in 24 hours, 4 minutes, do not display additional banner.
   * If the event ends in 23 hours, 59 minutes, banner should display "*Ends in 23 hours*"
   * If the event ends in 16 hours, 36 minutes, banner should display “*Ends in 16 hours*”
   * If the event ends in 1 hour, 59 minutes, banner should display “*Ends in 1 hour*”
   * If the event ends in 1 hour, 1 minute, banner should display “*Ends in 1 hour*”
   * If the event ends in 1 hour or less, the banner should read "*Ends in less than 1 hour*"

###Marketing Seals

Marketing seals are added in Hautelook admin to certain events. If a marketing seal has been added in admin, an additional graphic on the Event Tile is required.

See comp - [Marketing Seal Comp](ADD INVISION LINK)

* Position the graphic at the top righthand corner of the tile.
  * **NOTE**: seals are always assigned at the event level.
  * **NOTE**: Event Tiles in the Ending Soon section (on All and Women) do not support marketing seals.
  * **NOTE**: Event images displayed under Also New Today will never include event seals as well.

##Promotion Tiles

Promotional tiles are scheduled in Hautelook admin [Promo CMS](https://admin.hautelook.net/promo-cms/schedule) and affect the positions and sizes of Event Tiles. Promotional tiles are returned via the /promotions API.

###Marketing Promo Banner

The Marketing Promo banner is returned from the /promotions API as  

```JSON
promo_placement: "ember_top_promo"
```

If a Marketing Promo Banner is returned as active: "true", it should appear below the header navigation.

* Asset will always extend the 960px wide but can vary in height.
  * **NOTE**: asset provided as an image and will never include live text.
 * **NOTE**: I believe we redefined the width from 962px to 960px when implementing on the new NR homepage.
* Destination link can be scheduled via admin and returned via promotions API:
  * If a link is scheduled for the placement, the entire asset should be clickable.
  * If a link has not be scheduled, just display the image.
* Promo banners can be targeted to display on specific event verticals (All Events, Women, Men, Kids, Home, and/or Beauty) using event_tab.

###Promo Carousel

The  Promo Carousel is returned from the /promotions API as  promo_placement: "ember_rotating_promo" If a  Promo Carousel is active: "true", it should appear to the right of Event Secondary Tile 2. See [Promotional Tiles - ember_rotating_promo](ENTER INVISION LINK) for placement.
* **NOTE**: When a Promo Carousel is live, the Event Secondary Tile 2


###Promo Grid Tile 1

###Promo Grid Tile 2

###Marketing Bottom Promo Banner


##Events Ending Soon


##Also New Today


##Upcoming Events
