# Subscriptions- creating and managing orders

This page describes how shops can setup unique subscriptions for individual customers, including which items are in the subscription, which schedule the subscription applies to and pausing and editing the subscription.

{% hint style="info" %}
 In this first version of the subscriptions feature, shops must setup subscriptions on behalf of their customers. There is no customer facing place where customers can setup their own subscription.
{% endhint %}

**Checklist of things to do before you create subscriptions for you customers:**

* Enable subscriptions in your [Enterprise Settings](../../basic-features/enterprise-settings.md#shop-preferences)
* Setup [shipping and payment methods](subscriptions-configuration.md#2-make-sure-you-have-shipping-and-payment-methods-setup)
* Have made contact with you customers to [get their details](subscriptions-configuration.md#3-gather-information-from-your-customers)
* Added your subscription customers to your [customer list](subscriptions-configuration.md#4-add-your-subscribers-to-your-customer-list).  
* Have contacted your customers to request that they [sign up for an account with OFN](subscriptions-the-customers-perspective.md#signing-up-to-ofn), and _if_ they will be billed with stripe, to request they [save their card and authorise your shop to charge it](subscriptions-the-customers-perspective.md#saving-credit-cards-and-authourising-charges).
* Created at least one [Schedule](subscriptions-configuration.md#5-schedules)

## 6\) Create subscriptions

Click on **Orders** in the blue horizontal menu and then select **Subscriptions** in the green sub-menu.

Click **+ New Subscription** to setup a recurring order for your customer.

![](../../.gitbook/assets/new-subscription-basic-details.png)

**Customer:** 

Select a customer from the drop-down list.

\* You can only create a subscription for a customer who is on your [Customer List](../shop-setup/customers.md).

**Schedule:** Select the schedule, or order cycle group, that this customer wants to subscribe to.

{% hint style="info" %}
You must have created a schedule of order cycles before you can create a subscription. Instructions [here](subscriptions-configuration.md#2-schedules).
{% endhint %}

**Payment method:** Select the customer’s preferred payment method. This must be either Stripe or a manual payment method such as cash. Paypal and Pin Payments are not supported for subscriptions.

**Shipping method:** Select the customer’s preferred shipping method.

**Begins at:** This is the date that the customer’s subscription will start to be generated. If this date is midway through an open order cycle in their schedule there will be an order generated for that order cycle. If not the first order will apply to the next order cycle which open in their schedule.

**Ends at:** After this date the customer’s standing orders will no longer be generated. This field is optional, if left blank the order will continue to be generate indefinitely. 

How exactly does the end date interact with the OC dates? If the customer's subscription end date is after the opening date of an OC in their schedule, but before the end date of the OC, there won't be an order generated. The last order will only be generated for the last order cycle which closes before their subscription end date. 

**Address:** Fill out the customer’s billing and shipping details. If there is saved customer shipping and billing details in your customers page, this information will load automatically.

![](../../.gitbook/assets/new-subscription-address.png)

{% hint style="info" %}
Note: If you update the customer's address in the Customer page, this change won't automatically carry through to their subscription, so you'll need to update it here too.
{% endhint %}

**Add Products**

You can add any products that are in future Order Cycles that are within the schedule. You can't add products to a subscription if they aren't in any future order cycles within the schedule that the customer is subscribing to.

![](../../.gitbook/assets/new-subscription-add-products.bin)

#### Summary

Check that details are correct and then click **Create Subscription** or **Cancel**.

{% hint style="info" %}
Warning! If you have an order cycle which is open and assigned to a schedule, the moment you create a subscription for a customer to that schedule, an order will get created for them, and they'll be sent a confirmation email. If you're just setting up subscriptions, and don't want any orders to be triggered, make sure you don't have an open order cycle. See [8\) How subscriptions are processed](subscriptions-creating-and-managing-orders.md#8-how-subscriptions-are-processed) below for more details.
{% endhint %}

**What happens if the price of a product changes after the subscription is made?**

The prices of items within subscriptions will update and the customer will be charged according to the updated price.

**What if a product in a subscription is not available in an order cycle?**

When an item in a subscription is not available the customer will be alerted in their confirmation emails.

## 7\) Edit a customer’s subscription

### Edit the base subscription

From the **Subscriptions** page, click on the **edit** button next to the subscription you want to edit.

![](../../.gitbook/assets/edit-subscription.bin)

From here you can edit which products are in the subscription, the preferred shipping and payment methods, the starting and ending dates and the customer’s details.

{% hint style="info" %}
 You cannot change a subscription’s schedule. Instead the subscription must be recreated in the new preferred schedule.
{% endhint %}



### Edit one specific order

If you want to change a single upcoming order in a subscription you can click on the number in the customers’ orders column.

This will reveal all upcoming orders in the schedule, and you can then edit a specific order.

![](../../.gitbook/assets/edit-single-subscription-order.bin)

### Delete a subscription

From the **subscription** page, click the **cross** button next to the subscription you wish to delete. This will prevent any future subscriptions from being generated and delete this subscription permanently.

![Delete Standing Order](../../.gitbook/assets/delete-standing-order.png)

{% hint style="info" %}
 If you delete a subscription while there is an open order cycle you'll be asked whether you want to keep the customer's open order, or if they want to delete the current order.
{% endhint %}

### Pause a subscription

From the subscriptions page, click on the **pause** button next to the subscriptions you wish to pause. This will prevent all future orders in the subscription from being generated, until it is activated again. To un-pause a subscriptions, click on the play button.

{% hint style="info" %}
 If you pause a subscription while an order cycle is still open, you'll be asked whether you'd like to keep the current order or not. 
{% endhint %}

{% hint style="info" %}
If you un-pause a subscription while an OC is open an order will be generated for this customer if they're subscribed to that schedule.
{% endhint %}

![](../../.gitbook/assets/pause-subscription.bin)

## 8\) How subscriptions are processed

So once subscriptions are setup, how are they processed each time an order cycle opens and closes?

**1\) An OC within a schedule opens:**

* This triggers the creation of subscription orders for your customers who are subscribed to the schedule. 

{% hint style="info" %}
**BEWARE! The moment you open an order cycle within a schedule, an order will be created for each of your subscribers and they'll be emailed, so make sure you're ready! Double check you've setup your OC correctly and have updated your product availability before you open an order cycle.**
{% endhint %}

* The stocks level will be deducted accordingly at this time
* Each customer with a subscription order will get an email telling them that their order has been prepared.
* An email will be sent to the shop's notification email summarising how many subscription orders there are, and how many had issues \(e.g. insufficient stock\).
* During the time when the OC is open the customers may be able to edit their order \(depending on your [shop preferences](../../basic-features/enterprise-settings.md#shop-preferences)\)

{% hint style="info" %}
Note, if you create a subscription while there's an open order cycle in the schedule, an order will be immediately created for that subscriber.
{% endhint %}

**2\) The OC closes**

* When the Order cycle closes the subscription orders will be confirmed.
* If customers are paying with Stripe, their credit card will be billed at this time
* The customer will receive an email confirming that their order is complete.
* The shop notification email will get an email confirming how many subscription orders were processed. It will also mention any errors - such as a credit card that couldn't be billed.

### Planning for future subscriptions

There's two ways for planning the opening and closing of order cycles in your schedules. 

Regardless of which option you use, remember that the frequency that you create order cycles in your schedule will dictate how often the subscription reoccurs. E.g. If you create an order cycle for each week opening on a Monday, your customers will get weekly subscriptions.

**Manual option**

You can create order cycles in your schedule\(s\) on a one by one basis. How this would work is that when you're ready to open and order cycle  you'll check that you've updated everything outside of order cycles, such as your product availability, and any shipping method descriptions etc.

Then, you're ready you create the order cycle, either by cloning an existing one or creating a new one. You'll add in the product range and check the text fields of the order cycle \(such as the 'ready  for' date\). Also check that you've updated product availability. Then you can create the open order cycle. 

**Automatic option**

You can create future order cycles in advance, and set their opening and closing dates to correspond with each subscription date. To do this you can create a series of order cycles through cloning, and adjusting the opening/closing dates, and the text fields \(such as the 'ready for' dates\).

Then, as time passes your order cycles will open and close, triggering the creation and confirmation of your subscriptions. 

Just make sure that before the opening date of each order cycle you double check your product availability etc.

