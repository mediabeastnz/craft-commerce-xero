<p align="center"><img src="./src/icon.svg" width="100" height="100" alt="Xero plugin for Craft Commerce 2"></p>

# Xero plugin for Craft Commerce 2

> **ALERT**: This plugin has been deprecated in favour of <a href="https://github.com/thejoshsmith/commerce-xero">Xero for Craft Commerce 2 & 3</a> that supports OAuth 2.0.
>
> This plugin is no longer maintained and is for those still using the deprecated OAuth1.0a method of connecting to Xero.
>
> All new issues and pull requests should be created on the new repository.

## Overview
**NOTE: 👨‍💻This plugin is stable and fine to use in production however it's in active development so expect frequent updates while new features are added until v1.0.0.**

This plugin allows you to automatically send Commerce invoices into Xero including contacts, payments and even inventory updates.

You'll need to create a [private application](https://developer.xero.com) within Xero and then connect via OAuth using a consumer key, consumer secret and private (self signed) certificate.

You'll also need a Certificate store which can be downloaded from this repo for ease of use. It's generated from Firefox's own Cert store and updated often. [see here](https://github.com/bagder/ca-bundle)

Once connected the plugin allows you to map your Chart of Accounts (Account Codes) including:

- sales revenue
- accounts receivable
- shipping/develiery
- rounding

By default all fully paid orders will be pushed into the queue (you'll need to ensure you're processing the queue freqeuently) with a delay of 30 seconds (this is reduce the time customers spend waiting for their order to process) and then once the queue has dispatched the job, the invoice will be sent to Xero.

If you need to send existing orders to Cero you can do so by viewing an order and you'll see a "Send to Xero" button which will instantly send the order off to Xero. This button also currently acts as a way to see if an order is already in Xero.

### What fields are sent to Xero
Below is a list of fields that is sent to Xero. In future versions hooks/events will be avaialbe if you require more information to be sent.

**Contact**
- first name
- last name
- email

**Order**
- status (AUTHORISED)
- type (ACCREC)
- contact (as above)
- LineAmountType (Exclusive) (future versions will be configurable)
- Invoice Number (order referrence)
- SentToContact (invoices are marked as sent)
- Due Date (now)

**Line Items**
- account code (sales)
- description (product tile)
- quantity
- unit amount (item total)
- Item Code (sku) (if inventory is enabled)

**Shipping adjustments**
- same as above but account is set to you defined shipping account.

**Payment**
- account (receivable account)
- reference (order transaction reference)
- amount (total paid amount)
- date (date paid)

### Rounding
Due to how different systems calculate rounding if for whatever reason the order total is different to what Xero calculates, an additional line item to account for rounding is added in Xero. Please ensure you have this account code selected under settings.

### Multi environment settings
If you require different settings per environment the plugin ships with an example config file `xero-config.php` which should be copied into your config folder and renamed to `xero.php`. Once this is in place you r can define all the plugins settings for each environment.
Note if this file exists all settings will then be read from this file instead of whats in Craft.

> More detailed documentation to coming soon.

## Feature requests 🙏
As this plugin is still in active development now is a good time to suggest new features. Feel free to contact me via email or create a GitHub issue.

## Roadmap 🚀
- Improve documentation
- Configure Crafts new testing framework to ensure new features don't cause unexpected issues.
- Add multiple hooks/events so developers can further extend if required
- Refunds support
- Admin features like element actions, widgets and different syncing methods

## Installation
Either by the plugin store (search "Xero") or via composer.

`"thejoshsmith/craft-commerce-xero": "^0.9.3"`

## Requirements
This plugin requires Craft CMS 3.1.0 or later and Craft Commerce 2.0 or later.
