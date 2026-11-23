# Luna Labels

A web app for designing and printing prep labels on a **Bixolon SLP-DX220B** thermal label printer (shown in Bluetooth as **PrepWizardBix**). It runs in the browser from a single file, `luna-labels.html`. There's nothing to install.

---

## Quick start

1. Open `luna-labels.html` in **Microsoft Edge or Google Chrome on a computer**.
2. **Turn off Bluetooth on the PrepWizard tablet.** The printer accepts only one connection at a time.
3. Click **Connect printer** (top right) → **Bluetooth** → pick **PrepWizardBix**.
4. On the **Print** tab, tap **+** next to the labels you want, then press **Print** at the bottom.

> iPhone/iPad browsers can't reach printers. The preview inside the Claude app can't print either. Use the downloaded file in Edge or Chrome.

---

## Requirements

| | |
|---|---|
| Printer | Bixolon SLP-DX220B (203 dpi, up to 54 mm print width) |
| Labels | 2" × 1" by default. 2" × 2", 2" × 3", 2" × 4" and custom sizes are supported |
| Browser | Edge or Chrome on Windows, Mac, Linux or ChromeOS |
| Internet | Only needed for web fonts and Google Sheet sync. Printing works offline |

---

## Connecting the printer

- **Bluetooth (recommended):** **Connect printer → Bluetooth → PrepWizardBix**. The printer pairs as a Bluetooth LE device, so no COM port is needed.
- **USB:** **Connect printer → USB cable or COM port**, then pick the port.
- The dot next to **Connect printer** turns green when the printer is connected.

### Automatic reconnect
The app tries to reconnect to the last printer when it opens. If it can't, one tap on **Connect printer** opens the printer list. For automatic reconnect to work in Edge:

1. Go to `edge://flags` (in Chrome, `chrome://flags`).
2. Search **"new permissions backend for Web Bluetooth"** → **Enabled** → restart the browser.
3. Connect once more. After that the app reconnects on its own.

### Sharing the printer with PrepWizard
- **To use Luna Labels:** turn off Bluetooth on the PrepWizard tablet, then connect.
- **To go back to PrepWizard:** **Settings → Disconnect (let PrepWizard use it)**, or close the tab. Switch the printer off and on if PrepWizard still can't find it.

---

## Print tab

| Tab | What's in it |
|---|---|
| **Prep** | Items from your imported prep list or Google Sheet, with filters (Refrigerated, Room temp, Frozen, Hot, Other) |
| **Custom** | Labels you designed yourself. The 🗑 button deletes one (asks first) |
| **Batch** | Saved sets of amounts (e.g. "Morning"). **Load**, **Rename** or 🗑 delete |

- Use **− / +** to set how many of each label to print.
- **+ Save as batch** saves the current amounts under a name and clears them. Load the batch later from the **Batch** tab.
- If you've set amounts on a tab you're not viewing, that tab shows a small number.
- The **Print** button prints everything selected across all tabs. If the printer isn't connected, it says **Connect printer** instead.

---

## Design tab

### Adding things
- **Add text:** adds a text box using the same font and size as the last text you made, ready to type.
- **Add image:** fits the image to the label. Artwork made at the exact label size (e.g. 406 × 406 for 2" × 2") is placed dot-for-dot.
- **Upload a font:** add any `.ttf`, `.otf`, `.woff` or `.woff2` font. It's remembered with your labels.
- **Typing a label name** puts it on the label as the title automatically.
- **Add prep time**, **Add use-by** (set the days in the box) and **+ Today's date** add ready-made date lines.

### Toolbar (above the label)
- **Text selected:** font (each name shown in its own style), size, Regular/Bold/Italic, alignment, **Format**, **Size**, **Flip**, **Arrange**.
- **Image selected:** shading (**Photo**, **Line art**, **Logo**), **Format**, **Size**, **Flip**, **Arrange**.
- **Several selected:** change font, size, style and alignment for all of them at once.
- **Nothing selected:** label size, border and invert.

### Image shading
The app picks a shading mode automatically when you add an image. You can change it from the toolbar.

| Mode | Best for |
|---|---|
| Photo (dots) | Photos. Greys become fine dot patterns |
| Line art | Outlines and sketches. Keeps thin lines from disappearing |
| Logo (solid) | Solid shapes and logos |

### On this label (layers)
- The top of the list is the front-most layer, like Photoshop.
- **Drag** a layer to reorder it. **Double-click** it to rename it.
- The 🗑 on a layer deletes it.

### Moving, resizing, selecting
- **Drag** to move. Pink center guides appear and snap when the item is centered. Hold **Alt** to move freely.
- **Drag the handles** (corners and edge middles) to resize.
- **Double-click text on the label** to edit the words.
- **Shift/Ctrl-click**, drag a box, **Ctrl+A** or **Select all text** to select several items.

### Keyboard shortcuts
| Key | Action |
|---|---|
| Arrow keys | Nudge 1 dot (Shift = 10 dots) |
| Delete / Backspace | Remove selected |
| Enter | Edit selected text |
| Ctrl+D | Duplicate |
| Ctrl+A | Select everything |
| Esc | Deselect / finish typing |

### Saving
Press **Save label**. The label goes to the **Custom** tab, and the editor clears for the next one. Press **Edit** on any label to change it.

> The preview is exactly what prints: black or white dots at 203 dpi, enlarged on screen. Edges look blocky on screen but print smooth.

---

## Automatic dates

Type these into any text. They fill in when you print.

| Code | Prints | Example |
|---|---|---|
| `{date}` | Today's date | 11/23/26 |
| `{day}` | Day of week | MON |
| `{time}` | Current time | 9:51 AM |
| `{date+3}` | 3 days from now | 11/26/26 |
| `{date+4h}` `{time+4h}` | 4 hours from now | |
| `{time+10m}` | 10 minutes from now | |
| `{date+9mo}` | 9 months from now | |

`{day+N}` works the same way as `{date+N}`.

---

## Prep list (CSV import or Google Sheet)

### Import a file
**Settings → Import a .csv file** (or **Prep → Import a .csv file**). A review window lists every item. Untick anything you don't want, then press **Update list**. Importing a file adds and updates items. It never deletes.

### Columns
Row 1 must contain headers. The app recognizes:

| Column | Header contains | Required |
|---|---|---|
| Item name | `Item`, `Name` or `Product` | ✅ |
| Hold time | `Hold`, `Shelf life` or `Use by` | ✅ |
| Condition | `Condition`, `Storage` or `Preparation` | optional, printed on the label |
| Notes | `Notes` or `Limits` | optional, shown in the list (not printed) |
| Category | `Category`, `Type` or `Station` | optional. If missing, it's worked out from the condition |

Other columns (e.g. manual page) are ignored. An item with several conditions becomes one label per row, e.g. *Bacon – Refrigerated, opened*.

### Hold-time formats

| Written as | Use-by line |
|---|---|
| `10 minutes`, `4 hours`, `48 hours` | Date and time |
| `7 days`, `6 weeks`, `9 months` | Date |
| `end of day` | Today's date |
| `end of 7th day` / `End of day 7` | End of the 7th day, **counting the prep day as day 1** |
| `Use immediately` / `Serve immediately` | Printed as written |
| `Varies` | "HOLD TIME VARIES – SEE PROCEDURE" |
| `… or …, whichever comes first` | Extra line, e.g. "OR USE BY DATE IF SOONER" |
| `12 months from packing date` | "USE WITHIN 12 MONTHS OF PACK DATE" |

> ⚠️ Check hold times against your brand's manual before use. Labels are only as accurate as the list you import.

### Google Sheet sync (optional)
1. Create a sheet with the columns above.
2. **Share → Anyone with the link → Viewer**, then copy the link.
3. **Settings → Google Sheet item list** → paste → **Check sheet now**.

Each time the app opens, it compares your list to the sheet. If anything changed, a banner offers **Review and update**. Nothing changes without your approval. Labels you've restyled keep their design, and only the use-by line updates.

---

## Settings

| Setting | Purpose |
|---|---|
| Printer language | **ZPL** (default) or **EPL**. Switch if labels print blank |
| Darkness | 0–30 (ZPL only) |
| Bluetooth data channel | Appears after connecting if the printer has more than one. Switch if nothing prints |
| Extra Bluetooth service ID | Only for other printers. PrepWizardBix's IDs are built in |
| Download backup / Restore from backup | Save or move all labels, batches and fonts as a `.json` file |
| Current design as a file | Save the current label as `.png`, as printer code, or copy the ZPL |

---

## Where your data lives

- Labels, batches, fonts and settings are stored **in the browser on that computer**. They're not inside `luna-labels.html`.
- Opening a newer copy of the file **in the same browser** keeps everything.
- A different computer or browser starts empty. Clearing browsing data or using an InPrivate window loses the data.
- **Download a backup regularly** (Settings → Download backup). It's the only copy outside the browser.

---

## Extras

The heat-level labels (`heat-1-of-8-square.png` … `heat-8-of-8-square.png`) are made at exactly 406 × 406 dots for 2" × 2" labels. Set the label to **2" × 2"** first, then use **Add image**. The 2" × 1" versions (`heat-1-of-8.png` …) fit the standard roll.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Printer not in the Bluetooth list | Turn off the PrepWizard tablet's Bluetooth, switch the printer off and on, try again |
| "Couldn't connect" | Another device is connected. Close other tabs (including `edge://bluetooth-internals`) and turn off the tablet's Bluetooth |
| Blank label comes out | Switch **Printer language** (ZPL ↔ EPL) or the **Bluetooth data channel** in Settings |
| PrepWizard says "Printer not found" | Disconnect in Luna Labels (or close the tab), turn the printer off and on |
| Photo prints as blobs | Select the image and set shading to **Photo (dots)** |
| Thin lines disappear | Set shading to **Line art** |
| Text cut off | Change the font (it auto-fits) or drag a handle to shrink it |
| Labels missing after an update | Open the file in the same browser as before, or use **Restore from backup** |
| Asks to connect every time | Turn on the Edge/Chrome flag under *Automatic reconnect* |
