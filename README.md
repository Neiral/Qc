# Quiet Chat PWA

A mobile-first static PWA prototype for a single Discord channel.

## Files
- `index.html`: interface, PIN gate, Discord API/Gateway client
- `manifest.json`: install metadata
- `sw.js`: offline shell cache
- `icon.svg`, `icon-192.png`, `icon-512.png`: icons

## GitHub Pages deployment
1. Create a repository and upload these files to its root.
2. In GitHub, open **Settings → Pages**.
3. Choose **Deploy from a branch**, select `main` and `/ (root)`, save.
4. Wait for the Pages URL, open it on your phone.
5. In your browser menu choose **Add to Home Screen / Install app**.

## Discord setup
- Create a Discord application and bot in the Discord Developer Portal.
- Enable the **Message Content Intent** for the bot (if Discord requires it for your use).
- Invite the bot to your server with permission to view the channel, read message history, and send messages.
- Copy the bot token and the target channel ID into the app setup screen.
- Use `/show old 20` to request the latest 20 channel messages. The app accepts up to 100 due to Discord API limits.
- New messages are streamed through the Discord Gateway while the app is open/unlocked.

## Important limitations / risks
- **A bot token in local storage is not secure.** Anyone with access to browser storage or developer tools can copy it. Do not use a bot token for a valuable bot or share the device/browser profile. This app never writes the token into the repository, but it is plaintext in local storage.
- GitHub Pages has no backend. Browser-based Discord REST/Gateway access may be blocked or limited by Discord browser/CORS policies, and the gateway connection may disconnect while the PWA is backgrounded. This is a prototype, not a guaranteed always-on messenger.
- The six-digit PIN hash is stored locally. It is a convenience lock, not cryptographic protection for the chat or token.
- Browser/OS lifecycle events cannot guarantee a lock on every wake. The app locks when it receives visibility/blur/page-show events.
- The intentionally generic wrong-PIN screen is a UI behavior; incorrect PINs do not unlock the chat.
- Never use this for accessing messages or accounts without permission.

## Privacy
This is a static local-first app. Messages are only requested when you send `/show old N`; live messages are rendered while unlocked. The browser cache stores the app shell, not Discord messages.
