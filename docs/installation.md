# Installing the Deskcord Embed

Deskcord's **live chat widget** installs on any website with a single `<script>` tag — no SDK, no build step, no framework requirement. This guide covers the full install flow, framework-specific examples, and troubleshooting for the **customer support widget**.

## 1. Add the Deskcord bot to Discord

Before you can generate an embed code, the Deskcord bot needs to be in your Discord server. Adding it takes about a minute and creates the server that will act as your **help desk**. If you don't have a Discord server yet, creating one is free and takes about two minutes.

## 2. Subscribe

Run `/subscribe` in your Discord server. Choose between:

- **Solo** — $9.99/month, one support agent, unlimited domains and conversations.
- **Team** — $49.99/month, unlimited team members, unlimited domains and conversations.

Both plans include a 7-day free trial. You'll be redirected to Stripe for secure checkout.

## 3. Generate your embed code

Run `/setup` in Discord. This generates a unique script snippet tied to your server's `app_id` — the identifier that routes widget conversations to the correct Discord server.

## 4. Paste the embed on your website

Paste the generated snippet into your site's HTML, immediately before the closing `</body>` tag:

```html
<script>
  window.deskcord = {
    settings: {
      app_id: "YOUR_DISCORD_SERVER_ID",
    },
  };
</script>
<script src="https://cdn.deskcord.chat/deskcord.min.js"></script>
```

The widget loads asynchronously and renders a chat bubble in the bottom-right corner of the page. No further configuration is required for a working **live support chat** widget.

### Optional: custom API domain

If you're self-hosting or proxying the Deskcord API under your own domain, pass a `domain` setting:

```html
<script>
  window.deskcord = {
    settings: {
      app_id: "YOUR_DISCORD_SERVER_ID",
      domain: "https://your-custom-domain.example.com",
    },
  };
</script>
<script src="https://cdn.deskcord.chat/deskcord.min.js"></script>
```

If omitted, the widget talks to Deskcord's default API at `api.deskcord.chat`.

## Framework examples

The embed is plain HTML/JS, so it drops into any stack's global layout:

**Next.js (App Router)** — add to `app/layout.tsx`:

```tsx
<Script id="deskcord-settings" strategy="beforeInteractive">
  {`window.deskcord = { settings: { app_id: "YOUR_DISCORD_SERVER_ID" } };`}
</Script>
<Script src="https://cdn.deskcord.chat/deskcord.min.js" strategy="lazyOnload" />
```

**WordPress** — paste the snippet into your theme's `footer.php` before `</body>`, or use a "custom scripts" / header-footer plugin.

**Webflow** — add the snippet under Project Settings → Custom Code → Footer Code.

**Shopify** — add the snippet to `theme.liquid`, just before `</body>`.

**Plain HTML / static sites** — paste directly before `</body>` in every page, or in a shared footer include.

## Multiple websites, one subscription

There's no per-domain fee. Install the same embed code — same `app_id` — on every website or product you run, and manage every conversation from a single Discord server. This is especially useful for indie hackers running several products under one subscription.

## Restricting the widget to your domains (optional)

By default, your embed code will run on any site it's pasted into. To prevent someone from copying your script tag onto their own site, run:

```
/set-allowed-domains add yourdomain.com
```

You can add multiple domains. Development domains (e.g. `localhost`) are always allowed automatically, so local testing keeps working without extra configuration. List your current allow-list with `/set-allowed-domains list`, or remove one with `/set-allowed-domains remove yourdomain.com`.

## Customizing the widget after install

Run `/customize-widget` in Discord to set your brand color, header text, and branding. Changes apply instantly on your live site — no redeploy needed.

## Troubleshooting

**The widget isn't showing on my website**
- Confirm the embed code is pasted before `</body>`.
- Confirm your subscription is active.
- Check the browser console for blocked scripts (ad blockers occasionally flag chat widgets).
- Hard-refresh the page (Cmd/Ctrl + Shift + R) to bypass cache.

**Customer messages aren't coming through**
- Confirm your subscription is active (`/manage-subscription`).
- Confirm the `app_id` in your embed code matches your Discord server.
- Confirm your Discord server is online and the bot has permission to create threads in your destination channel (`/set-destination-channel`).

**I can't reply to customer threads (Solo plan)**
- On the Solo plan, only the user assigned via `/set-main-cs-member` can reply. Replies from anyone else are deleted with a DM explaining the upgrade path to Team.

---

Back to [README](../README.md) · See also: [Discord Commands](commands.md) · [FAQ](faq.md)
