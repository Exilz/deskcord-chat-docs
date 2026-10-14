# Identifying Logged-In Users

If your website has user accounts, you can tell the Deskcord widget who your visitors are. Identified users:

- skip the "introduce yourself" form,
- show up in Discord with their name, email and profile picture,
- with identity verification, find their current and past conversations on **every device and browser**, not just the one they first chatted from.

Deskcord still stores no message content: conversations live in your Discord server and are read from there when the user opens the widget.

> **Full guide:** [deskcord.chat/help/identity-verification](https://deskcord.chat/help/identity-verification?utm_source=github&utm_medium=docs) has code for Node.js, PHP / Laravel, WordPress, Python, Ruby on Rails, Go, Java and C#, frontend examples for React and Vue, and a ready-made prompt for AI coding agents if you don't code.

## 1. Turn on identity verification in Discord

```
/identity-verification enable
```

Only members with the **Manage Server** permission can run it. The bot replies privately with your **identity secret**.

- `/identity-verification rotate` replaces the secret. Use it if the secret ever leaks: the old one stops working immediately.
- `/identity-verification disable` turns the feature off.

## 2. Keep the secret on your server

Store it like any other API key, for example in a `DESKCORD_IDENTITY_SECRET` environment variable. **Never put it in your website's front-end code**: anyone who has it can sign in as any of your users.

## 3. Compute the user hash on your server

For each logged-in user, compute `HMAC-SHA256(secret, userId)` as a hex string. Use a stable id that never changes (your database id), not the email.

**Node.js**

```js
const crypto = require("crypto");
const userHash = crypto
  .createHmac("sha256", process.env.DESKCORD_IDENTITY_SECRET)
  .update(String(user.id))
  .digest("hex");
```

**PHP**

```php
$userHash = hash_hmac('sha256', (string) $user->id, getenv('DESKCORD_IDENTITY_SECRET'));
```

**Python**

```python
import hashlib, hmac, os
user_hash = hmac.new(os.environ["DESKCORD_IDENTITY_SECRET"].encode(), str(user.id).encode(), hashlib.sha256).hexdigest()
```

**Ruby**

```ruby
user_hash = OpenSSL::HMAC.hexdigest("SHA256", ENV["DESKCORD_IDENTITY_SECRET"], user.id.to_s)
```

## 4. Pass the user to the widget

**Server-rendered pages:** add `user` to the embed snippet, so the user is identified before the widget shows up:

```html
<script>
  window.deskcord = {
    settings: {
      app_id: "YOUR_APP_ID",
      user: {
        userId: "42",
        userHash: "<computed on your server>",
        name: "Ada Lovelace",
        email: "ada@example.com",
        avatarUrl: "https://example.com/avatars/ada.png", // optional
      },
    },
  };
</script>
<script src="https://cdn.deskcord.chat/deskcord.min.js"></script>
```

**Single-page apps:** call `identify()` once the user is logged in (the function exists once the widget script has loaded):

```js
window.deskcord.identify({
  userId: "42",
  userHash, // fetched from your backend
  name: "Ada Lovelace",
  email: "ada@example.com",
  avatarUrl: "https://example.com/avatars/ada.png",
});
```

Identify the user on **every page load** (or app start). A verified session lasts 24 hours and is refreshed each time you call it.

`avatarUrl` must be an `https://` URL. It's shown next to the user's messages in Discord.

## 5. Log the user out

```js
window.deskcord.logout();
```

Call it when the user logs out of your site. It removes the user's conversations and session from that browser, so the next person on a shared computer starts fresh. Calling `identify()` with a different user does the same automatically.

On server-rendered pages, also print `user: null` in the embed snippet when nobody is logged in. The first page after a logout then ends the chat session, even if your logout button doesn't call `logout()`. Don't call `logout()` for visitors who were never logged in: it would clear an anonymous visitor's ongoing conversation.

## Without identity verification

You can call `identify()` with only `name`, `email` and `avatarUrl`. The widget skips the intro form and Discord shows those details, but conversations stay tied to the visitor's browser, like an anonymous visitor.

## What happens to anonymous conversations?

If a visitor chats before logging in, that conversation is moved to their account when you identify them in the same browser. If they already had an open conversation, the anonymous one moves to their past conversations.

## Security notes

- Only the user id is signed. Name, email and avatar come from the page, so the Discord embed marks the **user id** as verified, not the email.
- Without a valid hash, nobody can read another user's conversations, even if they know that user's id.
- The widget's session token lives in a cookie your page's scripts can read. Like any chat widget, it is only as safe as your site: protect it against XSS.
- Combine it with [`/set-allowed-domains`](commands.md#set-allowed-domains) so your embed only runs on your own websites.

## Troubleshooting

**"Identity verification failed" in the browser console**
- Run `/identity-verification enable` if you haven't yet.
- Make sure you hash exactly the `userId` you pass to the widget (same string, no extra spaces).
- If you rotated the secret, update it on your server.

The widget keeps working in that case: the details just fill in the intro form.
