# Frequently Asked Questions

Answers to common questions about Deskcord's **live chat widget** and **Discord help desk** for websites.

## Getting Started

**How do I install Deskcord?**
Installation is simple: 1) Add the bot to Discord and authorize it on your server, 2) Subscribe to a plan with `/subscribe`, 3) Get your embed code with `/setup`, 4) Paste it on your website before the closing `</body>` tag. You'll be answering customers in under 5 minutes. Full walkthrough: [Installation](installation.md).

**Do I need a Discord server?**
Yes, but creating one is free and takes about 2 minutes. When you add the Deskcord bot, it guides you through the rest of the setup. Every customer conversation happens as a thread in your Discord server.

**How do I get the widget embed code?**
After subscribing, run `/setup` in your Discord server. Copy the generated script tag and paste it into your website's HTML before the closing `</body>` tag — the widget appears automatically.

## Using Deskcord

**How do I reply to customers?**
When a customer sends a message, a new thread appears in your Discord server's support channel. Reply in that thread like any normal Discord conversation — your message is sent instantly to the customer through the widget. You can reply from desktop or the Discord mobile app.

**Can I send images and files to customers?**
Yes. Attach images or files to your Discord messages in the customer thread, and they're sent through the widget. Customers can also send you images.

**How do I know when a customer messages me?**
You get a normal Discord notification, just like any other message. Enable Discord notifications on your phone to reply on the go — no separate app needed.

**Can I see conversation history?**
Yes. All messages are stored as Discord thread history — scroll the thread to see the full conversation. If you cancel Deskcord, all conversations stay in your Discord server forever.

**How can I customize my name and profile picture for support replies?**
By default, Deskcord uses your Discord name and avatar when replying to customers. You can set a different name/avatar per-server using Discord's [Server Profiles](https://support.discord.com/hc/en-us/articles/4409388345495-Per-Server-Profiles) feature, so you can maintain a professional identity on your support server while keeping your usual identity elsewhere.

## Plans & Billing

**How do I manage my subscription?**
Update your payment method, cancel, or view invoices through the Stripe customer portal (`/manage-subscription` in Discord, or the portal link with the email you subscribed with).

**What's the difference between Solo and Team?**
Solo: one designated person (assigned with `/set-main-cs-member`) can reply to customers. Team: unlimited team members can reply to any customer thread.

**Can I try before I pay?**
Yes — both plans include a 7-day free trial. Cancel anytime during the trial at no charge.

**What happens if I cancel?**
Your Discord server and all conversation history stay with you forever. You lose the widget on your website, but your data was never locked into Deskcord's platform.

**Can I upgrade from Solo to Team?**
Yes, anytime, via `/manage-subscription`. The price difference is prorated.

## Widget Customization

**Can I customize the widget's appearance?**
Yes — use `/customize-widget` to set your brand color, header text, branding, and widget position (bottom-left or bottom-right). Every accent in the widget updates to match, so it feels native to your site.

**Where does the widget appear on my site?**
As a chat bubble in the bottom-right corner by default — switch it to bottom-left with `/customize-widget`. It's mobile-responsive and works on all devices.

**Can I hide the widget on certain pages?**
Yes — conditionally load the embed script based on your own page/template logic to control where it appears.

## Privacy & Security

**Where is my data stored?**
In your Discord server, not on Deskcord's servers. No message content is stored by Deskcord. Discord handles infrastructure, encryption, and compliance.

**Do customers need Discord accounts?**
No. Customers interact entirely through the website widget and never see Discord or need an account.

**Is it GDPR compliant?**
Since all data lives in Discord (GDPR compliant) and Deskcord doesn't store messages, compliance is simplified — you control your data in your own Discord server.

**How can I prevent others from using my widget code on their site?**
Restrict your widget to specific domains with `/set-allowed-domains add yourdomain.com`. You can add multiple domains. This is optional but recommended.

## Troubleshooting

**The widget isn't showing on my website**
Check that: 1) the embed code is pasted before `</body>`, 2) your subscription is active, 3) your browser isn't blocking scripts, 4) you've hard-refreshed the page.

**I can't reply to customer threads (Solo plan)**
Only the user assigned via `/set-main-cs-member` can reply on the Solo plan. Replying as anyone else deletes the message and sends a DM explaining the upgrade path.

**Customer messages aren't coming through**
Verify: 1) your subscription is active (`/manage-subscription`), 2) the widget's `app_id` matches your server, 3) your Discord server is online and the bot has the right permissions.

**How do I contact support?**
Use the Deskcord widget on [deskcord.chat](https://deskcord.chat?utm_source=github&utm_medium=docs) — we dogfood our own product.

---

Back to [README](../README.md) · See also: [Installation](installation.md) · [Discord Commands](commands.md)
