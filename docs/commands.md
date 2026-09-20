# Discord Commands Reference

Deskcord is configured entirely through Discord slash commands in your server — there's no separate admin dashboard to log into. This is the full reference for every command available in the **Discord help desk** bot.

## `/subscribe`

Start your Deskcord subscription.

**Usage:** `/subscribe`

Opens a menu where you choose between the Solo ($4.99/month) or Team ($19.99/month) plan. You're redirected to Stripe for secure payment. Includes a 7-day free trial, no credit card required to preview.

## `/setup`

Get your widget embed code.

**Usage:** `/setup`

Generates your unique embed code to add the Deskcord **live chat widget** to your website. Copy the script tag and paste it into your site's HTML before the closing `</body>` tag. The widget appears automatically on every page that includes the code. See [Installing the Embed](installation.md) for full details.

## `/set-destination-channel`

Set your support channel.

**Usage:** `/set-destination-channel`

Run this in the Discord channel where you want to receive customer messages. This channel becomes your support inbox — every customer conversation appears here as a thread. The bot needs permission to create threads in this channel.

## `/manage-subscription`

Manage your active subscription.

**Usage:** `/manage-subscription`

Opens your Stripe customer portal, where you can upgrade or downgrade your plan, update payment methods, view invoices, or cancel.

## `/set-main-cs-member`

Assign the customer support seat (Solo plan only).

**Usage:** `/set-main-cs-member @user`

For Solo plan subscribers: designates which Discord user can reply to customer threads. Only the assigned user can send messages to customers — useful for solo founders who want to be the sole point of contact for support.

## `/resolve-conversation`

Close a customer conversation thread.

**Usage:** `/resolve-conversation`

Marks the current thread as resolved and archives it. The customer sees the conversation marked as completed in their widget. Use this when a support ticket is finished.

## `/customize-widget`

Customize your widget's appearance.

**Usage:** `/customize-widget`

Opens a configuration interface for your widget's brand color, header text, branding, widget position (bottom-left or bottom-right), and the offline message shown when no one's around to reply. Changes apply instantly on your website — no redeploy required.

## `/set-allowed-domains`

Manage allowed domains for security.

**Usage:** `/set-allowed-domains [add|remove|list] [domain]`

Controls which domains can use your widget embed code. Add domains to allow specific websites, remove domains to revoke access, or list all currently allowed domains. Optional but recommended. Development domains (`localhost`, etc.) are always allowed automatically.

---

Back to [README](../README.md) · See also: [Installation](installation.md) · [FAQ](faq.md)
