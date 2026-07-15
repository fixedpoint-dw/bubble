# Bubble Lab — Vernon Smith Asset-Bubble Experiment for the Classroom

A single-file, phone-friendly replication of Smith, Suchanek & Williams (1988) using their original market mechanism: a **continuous double auction**. Students join from mobile browsers with just a name; the instructor runs the market from the same page.

## How trading works (true to the original)

- During each period, trading is **live and continuous** — no turns.
- Anyone can **post a bid** (offer to buy 1 share) or **post an ask** (offer to sell 1 share). The best bid and best ask are visible to everyone.
- **Improvement rule** (as in SSW 1988): a new bid must beat the standing bid; a new ask must undercut the standing ask.
- Anyone can **accept** the standing bid or ask for an instant trade. A bid posted at/above the ask (or vice versa) executes immediately. After a trade, the book clears.
- Every trade is one share, and the full transaction tape for the period is visible to all.
- A period ends when the **timer** runs out (default 180s), when **every trader taps "I'm done"**, or when the instructor **forces it closed**. Then a random dividend (default 0/8/28/60¢, expected 24¢) is paid on every share, and the next period opens.
- After the final period, shares are worthless — only cash counts.

Names on quotes are shown by default for classroom energy; check **"Anonymous quotes"** in setup to match Smith's original anonymity.

## One-time setup (~5 minutes)

1. **console.firebase.google.com** → Add project.
2. **Build → Realtime Database → Create database** → any region → test mode.
3. Then open **Rules** and publish these permanent rules (they never expire):
   ```json
   { "rules": { "rooms": { ".read": true, ".write": true } } }
   ```
4. **Settings → General → Your apps → Web app (`</>`)** → register → copy the `firebaseConfig` and paste it into the block at the top of the `<script>` in `index.html`. Make sure `databaseURL` is present.
5. Push `index.html` to a GitHub repo → **Settings → Pages → Deploy from branch**. Share the URL (or a QR code) with the class.

## Running a session

- Students: open the URL, enter a name. Instructor: tap *Instructor login*, password `rationalbubble`.
- Configure periods, seconds per period, endowments, dividends; optionally show the fundamental-value line during play (off by default, as in the original).
- **Keep the instructor page open** — students trade with each other directly, but your device closes periods and pays dividends.
- Absent student? Tap **bench** next to their name so "everyone done" doesn't wait on them.

## After the game

Everyone sees the post-mortem: a scatter of **every individual trade** against the declining fundamental-value line, volume by period, bubble metrics (peak gap, average mispricing, turnover), dividend draws, a leaderboard, and discussion prompts. **Play again with the same class** restarts instantly — useful for showing Smith's finding that bubbles shrink with experience.
