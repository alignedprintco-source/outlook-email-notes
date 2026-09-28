# Email Notes for Outlook — Aligned Print Co.

A tiny, private Outlook add-in that gives you a notes panel on every email.

- **Notes on this email** — saved onto the message itself (paper type, quantity, quote, proof status…). Travels with the email; shows up on any device where you install the add-in.
- **Notes on this customer** — tied to the sender's address, so it shows up on *every* email from that customer.
- **At-a-glance tag.** Any email with a note gets tagged with a **Has Note** category, so you can spot it in your inbox list without opening the panel — no more wondering which emails you've already jotted something down on.
- Notes auto-save, live in your Microsoft 365 mailbox, and never leave Microsoft's servers. No third-party service, no subscription.
- Works in classic Outlook, new Outlook, Outlook on the web, and Outlook for Mac.

## One-time setup (about 15 minutes)

Outlook add-ins are just small web pages, so the two files need to be hosted somewhere with HTTPS. GitHub Pages is free and takes a few minutes.

### 1. Host the files on GitHub Pages

1. Create a free account at https://github.com (skip if you have one).
2. Click **New repository**. Name it `outlook-email-notes`, leave it **Public**, click **Create repository**.
3. On the empty repository page click **uploading an existing file**, then drag in everything from this folder: `manifest.xml`, `taskpane.html`, and the `assets` folder (drag the folder itself so the icons land in `assets/`). Click **Commit changes**.
4. Go to **Settings → Pages**. Under *Build and deployment*, set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**, click **Save**.
5. Wait a minute, refresh the page, and copy the URL it shows — it will look like `https://YOURNAME.github.io/outlook-email-notes`.
6. Test it: open `https://YOURNAME.github.io/outlook-email-notes/taskpane.html` in a browser. You should see "Open this inside Outlook." — that means hosting works.

### 2. Put your URL into the manifest

Open `manifest.xml` in Notepad and replace every `__HOST__` with your URL from step 5 (no trailing slash), e.g.
`https://YOURNAME.github.io/outlook-email-notes`. There are 7 of them — use Edit → Replace. Save it, and upload the edited `manifest.xml` to the repository too (Add file → Upload, it will replace the old one).

### 3. Install it into Outlook

Custom add-ins are installed once, at the mailbox level, and then appear in every Outlook you use with that account.

1. Sign in at https://outlook.office.com with your shop email.
2. Open any email, click the **…** (More actions) menu in the message → **Get Add-ins** (or **Apps → Get apps**).
3. In the left column choose **My add-ins**, scroll to **Custom Addins**, click **+ Add a custom add-in → Add from URL**.
4. Paste `https://YOURNAME.github.io/outlook-email-notes/manifest.xml`, click **OK**, then **Install**.
5. Restart classic Outlook on your PC. Open any email — there's now an **Email Notes** button on the ribbon (Home tab, far right). Click it, then click the **📌 pin** in the panel's top corner so it stays open while you click through your inbox.

If step 4 fails with a vague "installation is taking longer than expected" message, use the more reliable admin route instead (this is what worked for Aligned Print): Microsoft 365 admin center → Settings → Integrated apps → Upload custom apps → App type: Office Add-in → Provide link to manifest file → paste the manifest URL → Validate → Next → choose users → Finish deployment. Allow a few minutes (up to a few hours) for it to appear, then restart Outlook.

## Good to know

- **Limits.** Outlook caps a per-email note at roughly 2,400 characters and all customer notes combined at about 32 KB (≈ a few hundred customers with a short paragraph each). The panel shows a counter and warns before you hit either.
- **Replies and forwards.** Each message carries its own note. If you want a note to follow a whole job, put it in the customer note, or add it to the newest email in the thread.
- **Backups.** Notes are stored as hidden properties in your mailbox, so they're included in Microsoft's normal mailbox backup/retention. They are not visible to anyone you forward the email to.
- **Removing it.** Same place as step 3 → My add-ins → Custom Addins → … → Remove. Existing notes stay stored on the messages (invisible) and reappear if you reinstall.
- **The "Has Note" tag.** The first time you open an email that has a note, or the moment you type one, Outlook adds the **Has Note** category to it — that's what makes it visible in the inbox list. Clear the note text and the tag comes back off automatically. You'll also see **Has Note** if you ever open Outlook's Categorize menu; that's normal, it's just how the tag is implemented. If you ever want to change its color, right-click any tagged email → **Categorize** → **All Categories…**, select Has Note, and pick a new color — the add-in won't touch it again once it exists.
- **Older notes.** Emails you noted before this update don't get tagged until you open them once in the panel (that's what re-applies the tag). New notes are tagged immediately.

## Changing it later

Everything is in `taskpane.html`. Edit it, re-upload to GitHub, and Outlook picks up the change on next open — no reinstall needed. If you change `manifest.xml` (e.g. the button name), bump the `<Version>` and remove/re-add the add-in.
