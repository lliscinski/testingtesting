#FAQ Page Requirements


###General Information


Nordstrom Rack
* For syle requirements, please refer to current [NR FAQ Page](https://www.nordstromrack.com/faq)
* For copy, please refer to [NR FAQ Copy Page](/nrfaq)

HauteLook
* For syle requirements, please refer to current [HL FAQ Page](https://www.hautelook.com/support#faq_page)
* For copy, please refer to [HL FAQ Copy Page](/hlfaq)

###Functionality

#####Goal:

Allow customers to find answers for commonly asked questions in order to decrease customer service workload

* Under each section header, include the listed FAQs
 * When customer clicks a specific FAQ, the answer will be exposed below. Ensure that all subsequent items are pushed.
 * If an FAQ answer is exposed and the customer clicks on the FAQ, the answer will be hidden and all subsequent items are pulled.
 * If an FAQ answer is exposed and the customer clicks on a new FAQ, the currently exposed answer will be hidden and all subsequent items are pulled. At the same time the answer for the new FAQ will be exposed and all subsequent items are pushed.
 * Specific considerations
   * The answer to FAQ - *Does HauteLook charge sales tax?* includes URL [http://statelaws.findlaw.com/tax-laws/](http://statelaws.findlaw.com/tax-laws/) and this link needs to open a new window.
    * Under both ORDERS and SHIPPING & RETURNS sections, an initial set of FAQs is present with the option to see all. When customer clicks *See all \[HEADER TITLE] questions*, the remaining FAQs will be exposed,pushing subsequent items, and a *Close* option will be present at the bottom.
    * If customer clicks on *Close*, the extended FAQs will be hidden and will pull all susbsequent items.
    * At the bottom of the SHIPPING & RETURNS section, there is a link to the [Shipping & Returns](/ship-return-policy) relative URL.
    * Under the ACCOUNT - How do I update my email preferences? FAQ, there is a link to the [Shipping & Returns](/ship-return-policy) relative URL.
    * Under the ORDERS - How do I cancel if Member Care/Customer Care is closed? FAQ, there is a link to the [Email Preference Center](/account) relative URL.
    * **Investigate:** For answers to FAQs relating to shipping, the day requirement *MAY* be pulled in from an API since the date changes so regularly. This is included in the following FAQs:
      * SHIPPING & RETURNS - How long does it take to receive my order?
      * SHIPPING & RETURNS - Can I request overnight shipping?

* Back to top icon is persistent and follows the customer as they scroll down the site. It is located on the right side of the page.
* The contact us box on the top right of the page includes methods for the customer to contact customer services
  * Considerations:
    * LIVE CHAT shows a link for *Chat Now* that launches the CSR live chat modal.
    * EMAIL shows a link for *membercare@hautelook.com* which lauches an email modal addressed to membercare@hautelook.com
