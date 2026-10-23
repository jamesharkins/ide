# Load-In demo

One shared page per show. The act fills in its stage plot once, the input list builds itself, the venue's house gear checks it, and every question gets pinned to the gear it's about. The venue's week board shows every show's status.

- **Live demo:** https://claude.ai/artifact/98WX4cniBnZeEpmNhYWAuB (private until shared from the page's Share menu)
- **Source:** `index.html` is the whole app: Preact + htm from unpkg, no build step.
- **Data:** when it runs as the claude.ai page, it uses the page's shared database, so the venue and the act see each other's changes live. Opened anywhere else (a saved copy, a local file), it runs on the built-in sample week, and changes stay in that tab.

## What's in v1

1. **Plot builds the input list.** Drag gear onto the stage. Each item knows its inputs, mics, stands and 48V, so channels number themselves. The act's plot is saved for its next venue, and an act with a saved plot can load it in one tap.
2. **House check.** Every plot is checked against the room's channels, mixes, wedges, mic and DI stock, and house backline ("needs 26 inputs, house has 24"). The House gear page edits that list, and every show re-checks.
3. **Comments pinned to the gear.** Tap an item to ask about it. Open threads show as pins on the plot and in the input list.
4. **Week board.** Each show gets one status (Waiting on act, Open question, Ready to lock, Locked, Changed after lock), plus the first thing that is still open.
5. **Patch sheet.** A compact show-day view of inputs, mixes and backline.

Out of scope, as in the proposal: booking, contracts, ticketing, settlement. Email replies landing on the page are not built.

## Demo script (about 4 minutes)

Reset first: on the week board, click **Reset demo data**, then **Reset**.

1. **Week board (laptop).** "Monday: 4 of 7 shows locked. Each open one names what's missing." Point at Wed ("4 mixes asked, house has 3") and Sat (the drum riser question).
2. **Send the link.** On Fri, Velvet Cassette, click **Act link**. "One link per show, nothing to log into."
3. **Act on the phone.** Open that link on your phone. Tap **Use my saved plot**: 26 inputs from their last show, in one tap. The laptop's board flashes and reads "Not sent yet · House check: needs 26 inputs, house has 24."
4. **Settle it on the page.** On the laptop, open Velvet Cassette, tap the guitar amp, and pin: "We're 2 over. Can guitar go to one mic and perc to two?" The question pops up on the phone. On the phone, switch the guitar to **1 mic** and the percussion to **2 mics**, then tap **Send to The Low Room**.
5. **Lock it.** On the laptop, mark the question settled. The status reads Ready to lock, so click **Lock this advance**.
6. **The 4:40 pm problem.** On the phone, add Keys and a Wedge. The board flips to **Changed after lock: added Keys 2 (+2 inputs), added Wedge (mix 4)**, and the house check flags it again. No more "in RED below."
7. **Show day.** Open **Patch sheet**: "This is what Mara pulls up at 4:58."

Two devices are optional. On one screen, use **See the act's page** on any show to play the act.
