Weekly Sainsbury's food shop for Sian (UK, Europe/London time). This runs in TWO phases: first a short voice check-in with Sian, then the shop. Sian has ADHD: keep every message short, action first, no trailing questions beyond the one check-in prompt.

PHASE 1: CHECK-IN (do this as soon as you start, then STOP and wait)
1. Read the project doc `claude/meal-plan.md` with the Projects tool (project_read). It has the rules, the meal rotation with products, core staples, rotating extras, pantry list, "This week's extras / running low" and the log.
2. Draft 5 dinners for next week following the doc's rules (no repeats from the last 2 log entries, balanced mix).
3. Pick up to 8 "likely low" items to ask about: pantry items and staples that the log suggests haven't been bought for a while, plus anything already under "This week's extras / running low".
4. Send Sian ONE message with SendUserMessage, in this shape:
   "Shop time. Tap the mic and ramble for a minute: what's low, what you've got loads of, any dinner swaps.
   Draft dinners: 1) ... 2) ... 3) ... 4) ... 5) ...
   Worth checking: rice, olive oil, ...
   Say 'as is' to go with this."
5. End your turn and wait for her reply. Do NOT open the browser or change the doc yet.

PHASE 2: SHOP (after Sian replies, by voice or text)
6. Read her reply generously; it is dictated, so expect rambling and transcription slips. Extract: dinner swaps, items low/out (add), items she has plenty of (remove), extra one-offs. "As is" means no changes.
7. Build the shopping list: dinner ingredients + core staples + 3–4 rotating extras not bought last week + everything under "This week's extras / running low" + what she said is low, minus anything she said she has. Don't buy pantry items unless low.
8. Try the basket, time-boxed to about 5 minutes total:
   a. Load the built-in browser tools (ToolSearch query "mcp__remote-devices__Claude_Browser__", max_results 64) and open sainsburys.co.uk groceries.
   b. If you see a login page, CAPTCHA, verification code, or the site won't load after 2 tries: STOP using the browser immediately. Never enter or ask for her password. Go to step 9 with basket = "not filled".
   c. If logged in: book the coming Tuesday 7:00–8:00am slot (fallback 6:30–7:30am, then earliest before 9am; if none, say so and still fill). Clear leftover trolley items only if clearly from an old order. Add every item (exact product names from the doc where given; closest own-brand otherwise; flag substitutions). DO NOT check out or pay.
9. Update `claude/meal-plan.md` (project_read, edit, project_write the full content back to the same path): add a log line (delivery date, slot or "not booked", the 5 dinners, trolley total or "paste list given"), record what Sian said she has plenty of / is low on in the pantry section, clear "This week's extras / running low" back to a single "-", and fix any product names you confirmed.
10. Google Calendar: on the coming Tuesday, find the "Sainsbury's delivery" event (create it 07:00–08:00 Europe/London, location 82 Lyndhurst Way, London SE15 5AP, if missing) and set its description to "Weekly food shop delivery, 7:00–8:00am slot.\n\nDinners this week: <5 dinners separated by semicolons>."
11. Final SendUserMessage to Sian, short:
   - If basket filled: slot booked (or not), the 5 dinners, substitutions, trolley total, "Check out before the Sainsbury's cutoff."
   - If basket NOT filled: the 5 dinners, then a paste-ready list in a single code block, one item per line with quantity (e.g. "2 x semi-skimmed milk 4 pints"), grouped by aisle with no headings inside the code block, so she can copy it in one tap into Sainsbury's multi-item search or use it as a checklist. Then one line: "Basket wasn't filled because Sainsbury's is logged out in the Claude desktop browser. Log in there once to switch this back on." Then "Book the Tuesday 7am slot and check out."
