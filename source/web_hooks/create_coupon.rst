.. _web_hooks/create_coupon:
.. include:: /partials/common.rst

Create Coupon Web Hook
======================

Used for enterprise clients who want to give unique coupons to each visitor
and don’t want to manually upload a list of coupon codes to Talkable. In order
to create coupon codes for a coupon list automatically, Talkable can notify
a customer site which coupons should be created.

.. raw:: html

   <h2>When does Talkable call this web hook?</h2>

Suppose we have some codes in coupon list that are available for use. When the
number of coupons available drops below Threshold, the system tries to generate
15 new coupons in the background. If some person needs a coupon code, but there
are no coupon codes available, the system will try to generate one in the
foreground and give it to the person that requested it. In both cases coupons
are sent as a web hook and then inserted into the Talkable database only in case
when a web hook returns a successful response.

Threshold is dynamically calculated based on number of coupon codes used by
site in last 21 days. In this way Talkable coupon lists will always hold enough
available coupons to serve the site for 21 days if integration become broken.
Minimum Threshold is 20 coupons.

.. raw:: html

   <h2>Coupon Expiration timestamp</h2>

Talkable having a hard time making decision when the coupon we are creating should expire.
Only coupons that should be given on Friend Claim Page can have expiration and only when campaign offers are setup to expire.
Other coupons given as "Reward For Sharing" or "Advocate Reward for Referral" should not have expiration.

Expiration date for coupon on Friend Claim page is always greater than Advocate Claim Page expiration date + one day buffer.
So Talkable is making web hooks with expiration set to Friend Claim page expiration + 1 day when it has no coupons that match this criteria in its own database.

.. raw:: html

   <h2>Payload parameters provided for Create Coupon Web Hook</h2>

* **coupon_code** — coupon code
* **discount_amount** — discount amount
* **percentage_discount** — when true percentage discount should be created otherwise fixed discount
* **expires_at** — coupon expiration date
* **usage_limit** — number of usages for the coupon
* **coupon_list_id** — ID of the coupon list that need to be filled
* **coupon_list_name** — Name of the coupon list that need to be filled

.. raw:: html

   <h2>Sample payload</h2>

.. code-block:: javascript

   {
     "coupon_code": "WHT58574",
     "discount_amount": 10,
     "percentage_discount": false,
     "usage_limit": 1,
     "expires_at": "2014-04-14T06:17:14.309-07:00",
     "coupon_list_id": 1,
     "coupon_list_name": "$10 off"
   }

.. raw:: html

   <h2>cURL example</h2>

.. code-block:: bash

   curl --data 'key=<key>&payload={"coupon_code":"WHT58574","discount_amount":10,"percentage_discount":false,"usage_limit":1,"expires_at":"2014-04-14T06:17:14.309-07:00","coupon_list_id":1,"coupon_list_name":"$10 off"}' <url>

.. container:: hidden

   .. toctree::
