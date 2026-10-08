# The Griff: Outings & Events inquiry page

One self-contained page: `index.html`, plus an `images/` folder for photos. It needs no build step and no backend.

## 1. Before launch: confirm with the course

These items came from thegriffgolf.org (checked Oct 2026) or are not published. Unpublished ones are marked with a `CONFIRM` comment in `index.html`.

| Item | Current copy | Source |
|---|---|---|
| Price | $88/player ($68 green fee + $20 cart) | Host an Outing page. $68 matches the 2026 non-member 18-hole peak rate. |
| Shotgun start | 12:30–1:00 pm | Host an Outing page |
| Minimum | 80 players | Host an Outing page |
| Included | Green fees, carts, scoring & scorecards, cart signs | Host an Outing page |
| Outing Director phone | 203-531-6176 | Host an Outing page |
| Season dates | Generic ("during the golf season") | **Not published, so ask** |
| Deposit terms | "Confirmed in writing when you reserve" | **Not published, so ask** |
| Rain policy for outings | Lightning-horn rule + generic | Horn rule from Rules & Regulations; outing terms **not published** |
| Groups under 80 | "Send an inquiry anyway" | **Ask what they offer** |
| Who can book an outing | Not mentioned | **Ask.** Non-members can play (there are non-member rates), but membership is limited to Greenwich residents. |

### Left off on purpose
- **Bag service** and **food & beverage / clubhouse**: removed at the owner's direction. Note that the course's own "Host an Outing" page still lists bag service and says "the Restaurant has packages", and griffclubhouse.com is still online. Worth getting the Town's page updated so customers don't see conflicting information.
- **Food & beverage question** removed from the form for the same reason.

### Other facts used on the page (and where they come from)
- Named for former First Selectman Griffith E. Harris: Greenwich Free Press coverage of First Selectman history.
- Bunkers on holes 2, 3, 4, 6 and 7 rebuilt; MGA Public Links Qualifier hosted May 14, 2025: Griff Golf newsletter, June 2025.
- Multi-year tee box renovation (Kentucky bluegrass): "Golf Course Renovations" news post, Oct 29, 2025.
- Town men's, women's and junior tournaments: Events/Specials page.
- Pace of play (4¼ hours), dress code, no alcohol, lightning horn, own clubs and bag: Rules & Regulations page.
- Range balls $8 / $11 / $20 a bucket: 2026 fee schedule.

## 2. Photos: replace the stand-ins before launch

Every photo on the page is a **stand-in from Unsplash** (free license), there only so the design can be judged. None of them shows The Griff. Each one is marked with a `STAND-IN PHOTO` comment in `index.html`, and the footer says "Stand-in photography via Unsplash". Remove that footer line once real photos are in.

To swap a photo, put the file in `images/` and replace the Unsplash URL in its `src` (and `srcset` where present) with `images/your-file.jpg`.

| Slot | What to shoot | Size |
|---|---|---|
| Hero | Moody wide course shot, morning or late light. Text sits on the lower half. | 2400×1600 |
| Intro (portrait) | A green with the flagstick | 800×1000 |
| Event rows (3, phones only) | Charity group on the course · Carts lined up for a corporate outing · Club players on a green | 200×240 portrait |
| What's included background | Wide fairway (it sits under a dark overlay) | 2000×1300 |
| Add-ons (2) | Pro Shop prizes / a ball at the cup · The driving range | 300×300 |
| Gallery (7) | Mix of course shots and past outings (alternates landscape and portrait) | 1400 wide / 900×1125 |
| Inquiry side photo (desktop) | Tree-lined hole | 1400×1600 |

Use photos the course owns or has rights to. Compress them (e.g. squoosh.app) to under ~300 KB each, and update each `alt` text to describe the real photo.

## 3. Form: Formspree (works on GitHub Pages or embedded anywhere)

1. Create a form at formspree.io. Sign up with the inbox that should receive inquiries, ideally the Outing Director's.
2. Copy the form ID (the part after `/f/`) and replace `YOUR_FORM_ID` in `index.html`:
   `action="https://formspree.io/f/YOUR_FORM_ID"`
3. In Formspree's form settings, add any extra notification emails (e.g. a GM or backup inbox).

What's already wired up:
- **Subject line** is built from the answers, e.g. `Outing inquiry: Charity tournament, 80–120 players, 2027-06-12`, so the inbox is scannable.
- **Reply-To** is set to the customer's email automatically, because the field is named `email`. Hitting Reply goes straight to them.
- **Spam:** honeypot field `_gotcha`, plus Formspree's built-in filtering.
- **Inline success message** with no redirect. Until the form ID is set, submitting shows a "Setup needed" message instead.

### Optional extras
- **Auto-reply to the customer:** turn on Formspree's autoresponse in form settings. It's a paid-plan feature, so check current plans. Suggested text: *"Thanks for your interest in hosting an outing at The Griff. We've received your inquiry and the Outing Director will be in touch within 1–2 business days. Questions sooner? Call 203-531-6176."*
- **Text alert:** connect Formspree to Zapier or Make. On each new submission, send an SMS to the Outing Director's cell with name, event type, size and date.
- **Leads sheet:** use the same Zapier/Make step to append a row to a Google Sheet with columns `Received · Name · Email · Phone · Event · Size · Date · Status`. Default Status to `New`, and staff update it to `Contacted → Quoted → Booked / Lost`. Formspree's dashboard also keeps every submission and can export CSV, which works as a no-cost fallback.

### Using Netlify Forms instead
This only works if the page is hosted on Netlify. Change the `<form>` tag to
`<form id="inquiry-form" name="outing-inquiry" method="POST" data-netlify="true" netlify-honeypot="_gotcha">`,
add `<input type="hidden" name="form-name" value="outing-inquiry">`, and in the script change the `fetch` target to `"/"`. Also remove the `YOUR_FORM_ID` check.

## 4. Hosting

- **GitHub Pages:** put `index.html` and `images/` in a repo (or a folder like `/outings/`) and enable Pages.
- **Course's main site:** thegriffgolf.org runs on the Town's CMS. The simplest hand-off is to host this page (e.g. on GitHub Pages) and have the site admin link to it from "Host an Outing", or embed it:
  `<iframe src="https://YOUR-HOST/outings/" style="width:100%;height:2400px;border:0" title="Outing inquiry"></iframe>`
  A direct link is better on phones than an iframe.
- **Logo:** the header uses a text wordmark. Swap in the course's official logo file if they provide one.
