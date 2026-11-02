# The Higher Place website

Three files, no folders:

| File | What it is |
|---|---|
| `worker.js` | The whole website: pages, forms, admin dashboard and backend. You never edit it. |
| `wrangler.jsonc` | One small settings file. You paste your database ID into it once. |
| `README.md` | This guide (setup, content audit, picture list, launch checklist). |

It runs free on Cloudflare (a Worker plus a D1 database) with **no credit card**, deployed from GitHub. All content is managed in the dashboard at `/admin`.

---

## Set up (about 20 minutes, no extra services to sign up for)

Your database is already connected: the Database ID is filled in inside `wrangler.jsonc`, so you don't paste anything.

### 1. GitHub
1. Sign in at github.com → **New repository** → name it (for example `hpcweb7`) → choose **Private** → **Create repository**.
2. Click **uploading an existing file** (or **Add file → Upload files**), drag in the three files (`worker.js`, `wrangler.jsonc`, `README.md`) and click **Commit changes**.

### 2. Deploy on Cloudflare
1. Sign in at dash.cloudflare.com → **Workers & Pages → Create → Import a repository**.
2. Connect GitHub and choose your repository.
3. Name the Worker exactly **`hpcweb7`** (it must match `wrangler.jsonc`). Keep the other defaults and click **Deploy**.
4. When the build finishes you'll get an address like `hpcweb7.yourname.workers.dev`.

### 3. Two secret codes (needed once)
Worker → **Settings → Variables and secrets → Add** (type **Secret**), two of them:
* `ADMIN_PASSWORD`: a long code that opens first-time setup and acts as your **recovery key**. Save it somewhere safe.
* `SESSION_SECRET`: any random 40+ characters (mash the keyboard; you never type it again).

Save/deploy when asked.

### 4. First visit and your own admin login
1. Open your address once so the site loads its content.
2. Go to **`/admin`**. Type `admin` as the Login ID and your `ADMIN_PASSWORD` as the password.
3. Create **your own admin login**: a Login ID and a password (10+ characters). Email is optional. From then on you sign in with those.
4. Add more admins any time in **Account & admins**.

### 5. Your own domain (optional)
Worker → **Settings → Domains & routes → Add → Custom domain**. The domain must use Cloudflare's free DNS. The free `workers.dev` address costs nothing. Read the launch checklist first.

## What's new in this version
* **A different, useful pop-up on each page** (max one per page and four per visit; never while someone is typing; every pop-up fits the screen with its buttons in view, on phones too): welcome (first page of a visit; asks to subscribe, or says "welcome back" if they already have), visit invite (home), Save Sunday (New here), Come and see (About), question forms (Beliefs, Team, Young Adults, Students, THP Kids, Young at Heart), FAQ help (FAQs), newsletter (What's On, Sermons, Blog), apply (Internships), Gift Aid (Give), prayer meeting (Prayer), next step (Get involved), add-to-calendar (each event). Contact, Privacy and blog posts have none. Switch pop-ups on/off in **Settings → Pop-ups**.
* **Admin login with Login ID + password**, password reset by recovery key or by another admin (no email service or extra sign-ups), multiple admins and a built-in **How to…** guide. See below.
* **Home service card:** "Contact us" removed; the three remaining buttons are aligned and equal width.
* Event pages now offer **Add to my calendar** (`.ics` file) for that event.
* Earlier changes kept: celebration welcome, photo grid, quote banner, page transitions, language bar, YouTube feed, 3×3 blog videos.

## Updating from an earlier version
Keep using the **same database** (same Database ID in `wrangler.jsonc`) and all content and messages carry over; the new version updates what it needs automatically. Create the Worker `hpcweb7` from the repo, add the two secrets again (`ADMIN_PASSWORD`, `SESSION_SECRET`) and open the new address.

## Running costs
Everything uses Cloudflare's free plan at the time of writing: the Worker (100,000 requests/day) and D1 (5 GB storage, millions of reads/day). A church site stays far inside this. No card is asked for. You can confirm limits on Cloudflare's pricing pages.

## Using the dashboard (/admin): step by step

Sign in at `your-address/admin` with your **Login ID and password**. Everything you save appears on the website straight away. The dashboard also has a **How to…** page with these same guides.

**Change the service time, venue, address or contacts**
1. Click **Settings**. 2. Edit **Service and venue** (or **Contact and charity**). 3. Click **Save settings** at the bottom.

**Show an announcement bar:** Settings → **Announcement bar** → tick *Show*, type the message (and an optional link) → Save settings. Untick to remove.

**Add an event:** **Events → + Add event** → title, start date/time, place, description, optional picture and booking link → **Save**. It shows on Home and What's On and disappears after its date. (Two December services are saved as hidden drafts; open them, check the details and tick *Show on the website*.)

**Write a blog post:** **Blog posts → + Add blog post** → title, date, short summary, post text (blank line between paragraphs; `## ` before a line makes a heading) → **Save**.

**Add a sermon or video:** latest YouTube uploads appear automatically. To add one by hand: **Sermons & videos → + Add message** → paste the YouTube link → Save.

**Edit page wording (Our story, Young Adults, Kids…):** **Pages →** *Edit* → change text, quote, facts, picture → Save. **+ Add page** creates a new page and lets you choose its menu.

**Change pictures:** Upload on the page/event/setting itself, or use **Home photo grid** and **Settings → Pictures on pages**. Upload your logo in **Settings → Look and branding**.

**Quotes banner / pop-ups / giving links:** Settings → **Moving quotes banner**, **Pop-ups**, **Giving**.

**Messages, prayer requests, newsletter sign-ups:** **Messages** (new items have a dot) → open one → *Reply by email*, *Mark as read* or *Delete*. **Download spreadsheet (CSV)** exports them (e.g. into Mailchimp).

**Hide instead of delete:** untick *Show on the website* and Save.

**Reorder things:** items with an *Order* box (FAQs, values, team…) show smallest numbers first.

### Forgot your password? (no email service needed)
* On the sign-in screen click **Forgot your password?**, then enter your Login ID, your **recovery key** (the `ADMIN_PASSWORD` saved in Cloudflare) and a new password.
* Or ask another admin to open **Account & admins** and click **Reset password** beside your name.
* Lost the `ADMIN_PASSWORD` too? In Cloudflare, Worker → **Settings → Variables and secrets**, set a new `ADMIN_PASSWORD`, then use the recovery key option.

### Adding or removing admins
**Account & admins** → *Add another admin* (Login ID and a temporary password; email optional). Remove others with *Remove*. Changing a password signs that account out everywhere.

### Locked out completely?
Use the recovery key (option 2 above). If you've lost the `ADMIN_PASSWORD` too, open Cloudflare → Worker → **Settings → Variables and secrets**, set a new `ADMIN_PASSWORD`, then use the recovery key option.

## Honest limitations
* Pictures are stored in the database (card-free file storage isn't available), so each is limited to about 500 KB after automatic shrinking. Fine for web.
* No on-site search, no recurring-event engine (weekly gatherings are listed separately), no analytics (kept off for privacy and cost).
* The Vision 2030 PDF can't be stored here: upload it to Google Drive (or similar), copy the share link, and paste it in Settings → Links.
* Passwords are stored as salted PBKDF2 hashes (25,000 rounds, chosen to fit the free plan's processing limit). Use a long, unique password.
* On the free plan each request has a small processing limit. Pages measured about 1 ms in testing, far below it. If you ever see "Error 1102", tell me.
* I tested the single `worker.js` file with 80+ automated checks against a test database (all pages, forms, login, add/hide events, announcements, picture upload). I could not run it on a real Cloudflare account or view it in a real browser from here, so please click through every page after your first deploy and report anything odd.

---

## Content audit (old site → new site)

Old paths were kept wherever possible, so most links keep working.

| Old URL | New URL | Action |
|---|---|---|
| / | / | Rebuilt |
| /awareness (New Here?) | /awareness | Migrated + working form |
| /about | /about | Migrated |
| /beliefs | /beliefs | Migrated unchanged |
| /ourstory | /ourstory | Migrated |
| /dreamteam | /dreamteam | Migrated; other team names/photos needed |
| /s/Vision-2030-Multiplication.pdf | redirects to the link you set in Settings | **Add your link** |
| /help | /help | FAQs migrated |
| /youngadults, /youngpeople | /youngadults | Migrated; /youngpeople redirects |
| /students | /students | Migrated |
| /thp-kids | /thp-kids and /safeguarding | Migrated |
| /new-page-85 | /young-at-heart | Migrated; 301 redirect |
| /pastor-pauls-blog + 5 posts | /pastor-pauls-blog/… | Migrated in full; old post URLs redirect |
| /calendar | /calendar | Rebuilt; **events must be re-entered** (old calendar loads dynamically) |
| /sermonslibrary | /sermonslibrary | Not fully readable; 4 YouTube links from blog posts added; add the rest |
| /internships | /internships | Migrated (5 roles, 10 FAQs, quote) |
| /prayer | /prayer | Migrated + request form |
| /giving | /giving | Migrated; PayPal, bit.ly, CAF, Gift Aid links unchanged |
| (new) | /privacy /cookies /accessibility /safeguarding | **Drafts: need approval** |

Kept external services: PayPal, bit.ly giving link, CAF Donate, Gift Aid and internship Google Forms, ChurchSuite forms, Mailchimp, YouTube, Facebook, Instagram.

### Facts for the church to confirm
1. **Service time is inconsistent on the old site:** home and New Here say 10:15 AM; FAQs, Young Adults and Kids say 10:00 AM (kids check-in 9:45). The new home page uses 10:15 AM; FAQ wording is preserved as published. Confirm and edit in Settings and FAQs.
2. YouTube livestream at 10:00 AM, removed after 4 PM Sunday (from FAQs).
3. Friday prayer: no time on the FAQ; the July 2026 blog says 7:15–8:15 PM at GSU Room 025.
4. Young Adults Life Group (Tuesdays 7:30–8:30 PM, bi-weekly): the old page said "on break until early September"; that line was removed as out of date.
5. Christmas (13 Dec) and New Year's Eve (31 Dec) services come from an April 2026 forward look: saved as hidden drafts, venue/time unknown.
6. Titles, dates and speakers for the 4 seeded videos (titles taken from link text).
7. Bank details and charity number 1173023 were copied from the old site. Keep the GitHub repo **Private**.
8. Safeguarding lead (Adewale Adesanya, ade@thehigherplaceuk.com) from the Kids page.
9. Membership of Evangelical Alliance and Single Friendly Church Network.
10. Isabella's internship quote (Chief of Staff): confirm she agrees to its republication.
11. Only the pastors are named on the old team page; add other team members/trustees if wanted.
12. Privacy, cookie, accessibility and safeguarding pages are factual drafts of what this site does; please review (including how long you keep messages).
13. Old blog posts mention dated events; they're kept as history.

## Picture checklist
Until a photo is uploaded, a designed colour-circle placeholder shows, so nothing looks broken. Only upload photos you have permission to publish, especially of children.

| Where (dashboard location) | Shape / size | Subject |
|---|---|---|
| Logo (Settings → Look and branding) | Transparent PNG, ~600 px wide, must show on dark navy | Official logo (old one was white) |
| Home photo (Settings) | Portrait 900 × 1200 | Congregation / worship / welcome |
| Pastors (Team → Paul and Debi Ilo) | Portrait 600 × 800 | Pastors Paul and Debi |
| Each ministry page (Pages → Picture) | Landscape 1600 × 1200 | That group |
| What to expect cards (3) | Landscape 1600 × 1200 | Welcome, service, kids |
| Events | Landscape 1600 × 1000 | The event |

Videos: paste the YouTube link under Sermons. No background hero video is used, to keep the site fast on mobile.

## Launch checklist
Before going live
- [ ] Settings: service time, address, contacts and links confirmed
- [ ] Upload logo, home photo, pastors photo; add current events
- [ ] Work through the facts list above; approve the four legal pages
- [ ] Click every menu item, button and external link on phone and laptop
- [ ] Send a test message from each form; check it arrives in Messages
- [ ] Repo is Private; ADMIN_PASSWORD is long and unique

Going live
- [ ] Add the custom domain in Cloudflare; wait for it to turn active
- [ ] Open /sitemap.xml and /robots.txt
- [ ] Add the site to Google Search Console and submit /sitemap.xml
- [ ] Update Google Business Profile, YouTube, Facebook and Instagram links

After launch
- [ ] Check Search Console for errors in weeks 1–4; check Messages daily
- [ ] Monthly: Messages → Download CSV as a backup
