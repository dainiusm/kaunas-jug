# How to Add a New Kaunas JUG Event

This document describes every change required to add a new JUG meetup to `index.html`. It is written for AI use: follow the steps in order.

---

## Overview of what changes

When a new event is announced, two sections of `index.html` are updated:

1. **The jumbotron** (`<!-- ACTIVATE JUMBOTRON ... -->` block, ~line 229) — the prominent event announcement shown above the events list. Toggle visibility via inline style.
2. **The past events table** (`<h3>JUG Events List</h3>` section, ~line 291) — one new `<tr>` is prepended at the top of the table body (after the `<tr>` header row).

Optionally, sponsor logos in the **sponsor bar** (~line 91) are updated when a sponsor changes.

After the event, an **archive file** `index{N}.html` may be created as a snapshot of the live page.

---

## Step 1 — Update the jumbotron

The jumbotron block starts at:
```html
<!-- ACTIVATE JUMBOTRON ONLY ON EVENT TICKET SALE 'display: block', otherwise 'display: none' -->
<div class="jumbotron" style="display: none;">
```

### 1a. Make the jumbotron visible
Set `style="display: block;"` (change from `none`).

### 1b. Update event number and ticket link
Replace the commented-out ticket link and update the `<h1>` event number:
```html
<h3 style="text-align: center;">Grab your <a href="https://kaunas-jug{N}.eventbrite.com/">ticket here!</a></h3>
<h1>Kaunas JUG #{N}</h1>
```

Replace `{N}` with the new event number (e.g. `62`).

If the event starts at a non-standard time (not 19:00), add a note:
```html
<h1>Kaunas JUG #{N} <small style="color: darkred;">(starts at 18:00)</small></h1>
```

### 1c. Update the Eventbrite widget
The widget block contains **three** places where the Eventbrite numeric event ID must be updated — they must all use the same ID:

```html
<div id="eventbrite-widget-container-{EVENTBRITE_ID}"></div>

<script src="https://www.eventbrite.com/static/widgets/eb_widgets.js"></script>

<script type="text/javascript">
    var exampleCallback = function() {
        console.log('Order complete!');
    };

    window.EBWidgets.createWidget({
        widgetType: 'checkout',
        eventId: '{EVENTBRITE_ID}',
        iframeContainerId: 'eventbrite-widget-container-{EVENTBRITE_ID}',
        iframeContainerHeight: 425,
        onOrderComplete: exampleCallback
    });
</script>
```

Replace `{EVENTBRITE_ID}` in all three locations with the numeric ID from the Eventbrite event URL (e.g. `1974743014515`).

**Last used widget ID (JUG #61):** `1974743014515`

---

## Step 2 — Add the new event row to the events table

Insert a new `<tr>` as the **first row** in the table body — directly after the `<tr>` header row (the row with `<th>Date</th>`, `<th>Event</th>`, `<th>Slides and Photos</th>`).

```html
<tr>
    <td>{YYYY-MM-DD}</td>
    <td><a href="https://kaunas-jug{N}.eventbrite.com">Meeting #{N}</a></td>
    <td>
        <ul>
            <li><a href="javascript:alert('Comming soon...')">Talk Title - Speaker Name, Role (Company)</a></li>
            <li><a href="javascript:alert('Comming soon...')">Talk Title - Speaker Name, Role (Company)</a></li>
        </ul>
    </td>
</tr>
```

### Talk link lifecycle
| State | Link value |
|---|---|
| Slides not yet available | `javascript:alert('Comming soon...')` |
| Event happened, no slides | `javascript:void(0)` |
| Slides available (PDF) | `./material/meetup{N}/filename.pdf` |
| Slides available (external) | actual URL (YouTube, SlideShare, GitHub, etc.) |

### Speaker entry format
```
Talk Title - Speaker Name, Job Title (Company Name)
```

Example:
```html
<li><a href="javascript:alert('Comming soon...')">Structured concurrency - Audrius Mičiulis, iOS Developer at Devbridge/Cognizant</a></li>
```

---

## Step 3 — Update sponsors (only if a sponsor changes)

The sponsor bar is in the `<div class="col-md-10">` block (around line 91), inside `.row.row-valign` divs. Each sponsor is:
```html
<div class="col-sm-3 col-xs-6">
    <a href="{COMPANY_URL}"><img src="img/friends/{LOGO_FILE}" class="logocont" style="height: {H}px;" alt="{COMPANY_NAME}"/></a>
</div>
```

- To **deactivate** a sponsor: wrap the entire `<div>...</div>` in `<!-- ... -->`.
- To **activate** a sponsor: remove the `<!-- ... -->` wrapper.
- To **add** a new sponsor: add the logo file to `img/friends/` and add a new `<div>` entry.
- Logo heights vary by logo aspect ratio; typical values: 18–48px.

**Currently active sponsors (JUG #61):**
- Cognizant (`cognizant_logo.jpg`, 40px)
- JetBrains IntelliJ IDEA (`IntelliJ_IDEA.png`, 48px)
- Juvare (`juvare_logo.png`, 40px)

---

## Step 4 — Archive the current page (after event or at launch)

Copy `index.html` to `index{N}.html` as a historical snapshot. This is done selectively (not every event). The file name matches the event number of the content being archived.

```bash
cp index.html index{N}.html
```

---

## Step 5 — After the event: hide the jumbotron

Once the event has taken place and no new event is ready to announce:
```html
<div class="jumbotron" style="display: none;">
```

Update the talk links in the events table from `javascript:alert('Comming soon...')` to either real slide links or `javascript:void(0)`.

---

## Current state (as of JUG #61)

| Field | Value |
|---|---|
| Last event | #61, 2025-11-27 |
| Next event number | #62 |
| Eventbrite URL pattern | `https://kaunas-jug62.eventbrite.com/` |
| Archive files present | `index60.html` |
| Jumbotron state | `display: none` (no active event) |

---

## Complete jumbotron block template for a new event

```html
<!-- ACTIVATE JUMBOTRON ONLY ON EVENT TICKET SALE 'display: block', otherwise 'display: none' -->
<div class="jumbotron" style="display: block;">
    <div class="row">
        <div class="col-md-12">
            <h3 style="text-align: center;">Grab your <a href="https://kaunas-jug{N}.eventbrite.com/">ticket here!</a></h3>
            <h1>Kaunas JUG #{N}</h1>
        </div>

        <div class="col-md-12">
            <div id="eventbrite-widget-container-{EVENTBRITE_ID}"></div>

            <script src="https://www.eventbrite.com/static/widgets/eb_widgets.js"></script>

            <script type="text/javascript">
                var exampleCallback = function() {
                    console.log('Order complete!');
                };

                window.EBWidgets.createWidget({
                    widgetType: 'checkout',
                    eventId: '{EVENTBRITE_ID}',
                    iframeContainerId: 'eventbrite-widget-container-{EVENTBRITE_ID}',
                    iframeContainerHeight: 425,
                    onOrderComplete: exampleCallback
                });
            </script>
        </div>
    </div>
</div>
```
