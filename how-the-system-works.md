# How the AsOne Logistics system works

A guide to the system: what each part does, why it behaves the way it does,
and the things that catch people out the first time.

Written to be read by anyone who uses the system or needs to understand it —
warehouse staff, school clerks, Finance, Central Office, or somebody new
picking it up. You do not need to have seen it before.

**Last updated: 20 October 2026.** Everything below was checked against the
running system on that date. Where something is undecided or not built, it
says so rather than describing what it ought to do.

**First launch covers Production Orders and warehouse receiving.** Group
Orders (section 10) is hidden for now by AsOne's decision of 14 October and
returns after the initial launch; the section is kept and marked.

---

## Contents

| | |
|---|---|
| [1](#1-what-the-system-is-for) | What the system is for |
| [2](#2-the-five-roles) | The five roles |
| [3](#3-signing-in) | Signing in |
| [4](#4-how-stock-is-counted) | How stock is counted |
| [5](#5-control-numbers) | Control numbers |
| [6](#6-garments-sizes-and-skus) | Garments, sizes and SKUs |
| [7](#7-prices) | Prices |
| [8](#8-uniform-kits) | Uniform kits |
| [9](#9-loading-the-catalogue-from-a-spreadsheet) | Loading the catalogue from a spreadsheet |
| [10](#10-group-orders) | Group orders |
| [11](#11-production-orders) | Production orders |
| [12](#12-receiving-from-a-tailoring-centre) | Receiving from a Tailoring Centre |
| [13](#13-inventory-and-stock-corrections) | Inventory and stock corrections |
| [14](#14-stock-history) | Stock history |
| [15](#15-school-orders-picking-and-shipping) | School orders, picking and shipping |
| [16](#16-backorders-and-transfers) | Backorders and transfers |
| [17](#17-reports) | Reports |

---

## 1. What the system is for

AsOne runs three Tailoring Centres in rural Uganda that make school uniforms.
From the 2027 school year, uniforms are made between September and December
of the previous year, held in two warehouses, and withdrawn by the schools as
students need them.

This system is the record of all of that: what a uniform costs, what was
ordered from the Tailoring Centres, what arrived, what is on the shelf, and
what went out to which school.

It is a **standalone system**. It is not connected to any accounting or other
AsOne system, and the price a SKU sells for is the same as what it cost.

The work is delivered in three phases:

| Phase | What it covers |
|---|---|
| **1** | Inbound — group orders, production orders, receipts |
| **2** | Inventory adjustments and warehouse transfers |
| **3** | Outbound — school orders, picking, shipping |

---

## 2. The five roles

Everyone holds exactly one role. The role decides both **which screens they
see** and **whose data they see**.

| Role | Sees which sites | In one sentence |
|---|---|---|
| **Program Lead** | All | Runs the operation and sets up the catalogue. |
| **Operations Manager** | All | The same access; day to day, the person running production and the warehouses. |
| **Warehouse Staff** | Their own warehouse | Receives from the Tailoring Centres, picks, packs and ships. |
| **School Staff** | Their own school | Places student orders and tracks what has shipped. |
| **Finance** | All | Posts every inventory adjustment and reads the costed reports. |

Two consequences worth knowing before you start:

**A Program Lead cannot correct a stock miscount.** AsOne's access matrix
gives inventory adjustments to Finance alone, so a lead who finds a wrong
quantity has to ask Finance to post it. The warehouse staff who do the
counting cannot post the result either. This is recorded as an open question
with AsOne, because the counting happens at the warehouse and not in Finance.

**Warehouse staff can see past their own site in exactly one place** —
transferring an order to another warehouse. Nowhere else. That exception
exists because a transfer is meaningless if the clerk cannot see which
warehouse is receiving it.

**If a screen is empty, check the account's site first.** Site scoping denies
by default: a warehouse account with no warehouse assigned sees nothing
rather than everything.

---

## 3. Signing in

Everyone signs in with **their own email address and password**. There are no
shared accounts — every transaction records who did it, and that only works
if accounts belong to people.

**Getting in for the first time:**

1. An administrator creates the account and sets its role and site.
2. A password is generated and **shown on screen once**. It is never emailed.
   The administrator passes it to the person directly.
3. The person gets an email saying the account exists — no password, no code.
4. They sign in with the password they were given. That emails them a code.
5. They enter the code. It confirms their email address **and** signs them in.
6. They are then asked to choose a password of their own.

From step 4 onwards this is the ordinary sign-in everyone does every time.
The only difference on the first one is that the code doubles as the address
confirmation, and the screen says so.

If someone forgets their password, an administrator resets it and hands over
a new one the same way, and step 6 happens again.

**Why the password is never emailed:** the password and the code must not
travel down the same channel. If somebody else has the mailbox, emailing both
hands them the account.

**Every sign-in needs a code**, not just the first. Someone who is not in the
system is told they have no access rather than that their password was wrong.

---

## 4. How stock is counted

This is the single most important idea in the system.

**There is no "stock level" field.** Nobody types a quantity in, and nothing
stores "Namayemba has 250 white shirts". Every movement of stock writes a
permanent row — a receipt, a pick, a shipment, a correction — and a stock
level is **worked out by adding those rows up** whenever anybody asks.

So a shelf holding 155 shirts might read:

```
10 Oct   Receipt      RC-100001   +150   level 150
16 Nov   Adjustment   ADJ-9002      +5   level 155
```

**Why it is built this way:** you can always answer "how did we get to this
number?" Every unit traces back to a document and a person. A stored level
could drift away from the history behind it, and nobody could tell which was
right.

What follows from it:

- **Nothing is ever edited or deleted.** A mistake is corrected by posting an
  opposite entry, so both the error and the correction stay visible.
- **A new SKU reads zero**, because nothing has moved yet. That is correct,
  not a fault.
- **The level is always current.** There is no overnight recalculation and
  nothing to rebuild.

### The three stock statuses

A unit is in one of three states, and the ledger says which:

| Status | Meaning |
|---|---|
| **Available** | On the shelf, free to be ordered |
| **Picked** | Pulled for a specific order, still in the building |
| **Shipped** | Gone to a school |

This is why a single pick writes **two** rows on the same day at the same
warehouse — one taking units out of Available, one putting the same number
into Picked. Without the status those look like a contradiction. With it,
they read as stock reserved rather than stock gone.

---

## 5. Control numbers

Every document carries a number drawn from a database sequence, so numbers
are **never reused** and two people creating something at the same instant
cannot collide.

| Prefix | Document | Example |
|---|---|---|
| `GO-` | Group order | `GO-100001` |
| `PO-` | Production order | `PO-100001` |
| `RC-` | Receipt from a Tailoring Centre | `RC-100001` |
| `SO-` | School order — **also the invoice number** | `SO-20001` |
| `SH-` | Shipment to a school | `SH-5001` |
| `WT-` | Warehouse transfer | `WT-5001` |
| `ADJ-` | Inventory adjustment | `ADJ-9001` |
| `TX-` | Stock ledger transaction | `TX-1000001` |
| `UNI-` | SKU | `UNI-PS-CHS-XS` |
| `KIT-` | Uniform kit | `KIT-NUR-B-DAY-XS` |

**The order number and the invoice number are the same number.** The school
uses the invoice number and the student's name to give the right parcel to
the right child, so there is no second numbering to keep in step.

**Gaps in the sequence are normal.** If something is cancelled, its number is
retired rather than reissued. A missing `SO-20004` does not mean an order was
deleted.

---

## 6. Garments, sizes and SKUs

Three things that sound similar and are not.

**An item** is a kind of clothing — "Checked Shirt", "Grey Shorts". It
carries the price list it appears on and the price. It used to carry a
colour and a class band as well; AsOne dropped both in October 2026, and
the colour is in the name anyway — "Grey Shorts".

**A size** is XS, S, M, L, XL or XXL. Socks and neckties are **OS**, one
size, which fits any kit. Sizes are maintained under **Settings → Sizes**,
where the sort order matters more than it looks: sizes do not sort as text,
and alphabetically L lands between XS and M.

**A SKU** is an item in a size. It is what gets counted, ordered and
picked, and it is the only one of the three that appears in the warehouse.

A SKU number is made of four parts:

```
UNI - PS - CHS - XS
 |     |     |    └── size
 |     |     └─────── item code
 |     └───────────── price list
 └─────────────────── always UNI
```

Reading `UNI-PS-CHS-XS` tells you it is a Primary checked shirt in XS
without looking anything up. The number is **assigned once and never
changes**, because it is printed on shelf labels and pick lists.

### The price list in the number

| Code | Means |
|---|---|
| `PS` | Primary |
| `HS` | High School |
| `ALL` | Both lists — socks, neckties |

It is there so that items of the same name on the two lists stay apart:
`UNI-PS-SWT-XS` and `UNI-HS-SWT-XS` are different sweaters, priced
separately.

> **Numbers changed in October 2026.** They used to carry a class band and a
> colour — `UNI-NUR-CHS-XS-CHK`. When AsOne dropped both, items that differed
> only by band became one item, and their stock, orders and receipts were
> added together under the surviving number. Nothing was lost; the totals are
> the same. Old numbers on paper printed before then will not match the
> screen — look the item up by name.

**There is one SKU per item and size.** Trying to add a second is refused,
naming the one that already exists. Two rows for the same shirt in the same
size would split its stock across two numbers and neither would show the true
quantity.

---

## 7. Prices

**Price sits on the garment, not the SKU.** Every size of a white shirt costs
the same. A size premium is not merely unbuilt — it is impossible in the way
the data is shaped.

**Prices are dated.** A price has a start date, and changing a price does not
edit the old one: it closes the old price off and opens a new one from the
date you choose. So a reprinted invoice still matches the original, and you
can set a price now that starts next term.

Two prices for the same garment cannot overlap in time.

A garment with no price today cannot be ordered, and anything that would show
a total shows a gap instead of a zero. A zero is a number somebody might
quote to a parent.

### Agreed Price, on an order

Group orders and production orders carry an **Agreed Price** on every line:
what AsOne will pay the Tailoring Centre for that garment, per unit, on
*this* order.

**It fills itself in.** Leave it blank and the system takes the price in
force on the order date. You type in it only when the centre agreed
something else — a negotiated rate for a long run, say. A garment with no
price on file has nothing to fall back on, so the screen says so and asks
for one; an order that cannot be costed cannot fund anybody.

**It is a snapshot, not a lookup.** The figure is copied onto the line when
the order is raised and is never recalculated. Reprice the garment in March
and a January order still reads what was actually agreed in January.

That is the whole answer to "what happens to existing orders when the price
list changes": nothing happens to them, by design. The new price applies to
orders raised from its start date onwards, the old orders keep their own
figures, and the costed reports still reconcile against what the centres
were funded. The group order's own screen says as much under its lines —
*"Prices were fixed when the order was raised and are not recalculated."*

Quantity × Agreed Price is the line total, and the order total is what the
Tailoring Centre is paid against.

---

## 8. Uniform kits

A kit is a bundle a school orders as one line instead of five — a starter kit
for a new student.

**No warehouse ever holds a kit.** Ordering one turns it into its component
SKUs, and from there everything downstream — availability, picking, packing,
the ledger — deals in SKUs alone.

A kit is defined by the cohort it is cut for: **class band, gender, day or
boarder, and size**. Those four decide everything else, and the kit number is
built from them:

```
KIT - NUR - B - DAY - XS
 |     |    |    |     └── size
 |     |    |    └──────── DAY or BRD (boarder)
 |     |    └───────────── B or G
 |     └────────────────── class band
 └──────────────────────── always KIT
```

Nobody types that number. Unlike a SKU number it is **not frozen** — move a
kit from Day to Boarder and the number follows, because a kit still numbered
`-DAY-` would be describing the wrong kit.

**There is one kit per combination.** A second Nursery / Boy / Day / XS is
refused, and the form says so as soon as the fourth field is set rather than
after the components have been chosen.

**The components offered are narrowed to the cohort.** A Nursery kit in size
M offers Nursery garments in size M, plus one-size items like socks — about
fourteen things rather than the whole catalogue. A boarder's kit carries the
casual and dorm wear a day pupil goes home for, so it holds several more
items than the day equivalent.

**A kit has no price of its own.** Its price is the sum of its components at
today's prices, with no bundle discount. If any component has no price today,
the kit shows as unpriceable rather than cheap.

---

## 9. Loading the catalogue from a spreadsheet

Garments, sizes, SKUs and prices can be imported from Excel or CSV rather
than typed in. **One row per garment**, not per SKU:

```
name,code,colour,colour_code,school_level,fit_group,sizes,unit_price,active_date
Checked Shirt,CHS,Checked,CHK,PS,NUR,XS;S;M;L;XL;XXL,24000,2026-01-01
```

That one row creates the garment, its six sizes, six SKUs and the price
together. Sizes are separated by semicolons. A blank `active_date` means
today.

`code`, `colour_code` and `fit_group` are what produce the five-part SKU
number. Leave them out and you get a shorter fallback number instead.

How it behaves:

- **All or nothing.** If any row is wrong, nothing is imported. You never end
  up half-loaded and guessing where it stopped.
- **Every error at once**, each with its spreadsheet line number — counting
  the header as line 1, so it matches what Excel shows.
- **Safe to run twice.** Re-importing the same file changes nothing.
- **Check first.** The screen runs a check before it will import, reporting
  what *would* happen and writing nothing.

**It is not a back door.** Imported data goes through the same rules as data
typed in. A spreadsheet cannot create something the system would otherwise
refuse.

A kit bill of materials can be imported the same way, one row per component.
The garments have to be loaded first, because components are matched to SKUs
that already exist — nothing in the catalogue is created from a kit sheet.

---

## 10. Group orders

> **Not in the first launch.** AsOne's call of 14 October 2026 cut the scope:
> "Production Orders and warehouse receiving will be the priority for the
> initial launch. Group Orders: temporarily hide this functionality... The
> Group Order workflow will be revisited after the initial launch."
>
> Group Orders is hidden from the menu, from the Create Production Order
> form and from the order's own screen. Nothing was deleted — the screens,
> the data and the API are intact, and one flag
> (`src/features/shell/launchScope.ts`) brings all of it back. This section
> describes how it works, for when it returns.

A group order is **the season's whole requirement, entered once** — the
consolidated total across all three Tailoring Centres. It is what funds them
at the start of the season.

It carries a line per garment with a quantity and a unit price. The prices
come from the price list in force on the order date, so changing that date
reprices the order.

**Its own lines never change.** Order 200 of the 1,000 skirts and the group
order still says 1,000. What moves is the comparison on its screen:

```
Requirement vs Ordered
UNI-HS-BSK-XS   requested 1,000   ordered 200   −800
```

So the original requirement survives as a record, with progress beside it.

Its screen has three parts:

| Panel | What it shows |
|---|---|
| **Requirement vs Ordered** | Every garment on either document, with what was asked for, what has been ordered, and the difference |
| **SKUs On This Order** | The group order's own lines, with prices |
| **Production Orders Raised** | The orders placed against it |

**Shortfalls are reported, not blocked.** Ordering less than the requirement
may be deliberate; ordering more may be safety stock. Neither is an error the
system should stand in the way of.

**A production order may ask for a garment the requirement does not list.**
The plan can be added to. That row appears in the comparison tagged *Not on
this requirement*, and nothing is added to the group order itself.

---

## 11. Production orders

A production order is **one warehouse's order on one Tailoring Centre**: the
centre, the destination warehouse, a due date, and lines of SKUs.

A warehouse has a primary Tailoring Centre but **may order from any of them**.

**In the first launch there is no group order field.** Every order is raised
on its own, which the system has always allowed. When Group Orders comes
back, the field returns as the first one on the form, and orders raised in
the meantime can be attached to a requirement from their own screen.

What the field does, for when it returns: it links the order to the
requirement it breaks down, which is what makes the comparison in section 10
work. An order that names no group order counts towards nothing, and the
requirement goes on reading as wholly unmet. Each line then shows how much
of that garment is **still outstanding**, so you can see you are ordering
200 of the 800 still needed.

**The fulfilment status is calculated, not typed.** The system adds up what
has actually been received against the order, which is what makes it read as
*Awaiting delivery*, *Partially received* or *Received* without anybody
maintaining a field.

**Cancelling is a status change, never a delete.** The document funds a
Tailoring Centre, so it has to survive being withdrawn — and an order that
has already had a delivery against it cannot be cancelled at all. Goods have
moved; the paperwork cannot pretend otherwise. Close it instead.

**Nothing new can be raised inside a cancelled group order** (for when group
orders return). A withdrawn requirement approves nothing, so it cannot be
broken down further: it is not offered on the create screen, and an order
aimed at one is refused. Orders raised *before* it was cancelled are left
alone — they were valid when made, and the cloth may already be cut.

Deciding what to ask a Tailoring Centre to make is a programme decision.
Warehouse staff can read the queue and receive against it, but cannot raise
one.

---

## 12. Receiving from a Tailoring Centre

The Tailoring Centres are **not users of the system**. They make the goods
and send them with a handwritten packing list.

The warehouse clerk records what arrived:

1. Choose the production order the delivery is against.
2. Enter the **packing list number** off the TC's sheet, exactly as written.
3. Enter the **date received** and the carrier or driver who brought it.
4. Count the goods and enter what **actually arrived**, line by line.
5. Leave **As per packing list** ticked if the sheet agrees with your count.
   Untick it only where they disagree, and give a reason.

Saving it records the receipt **and posts it to the ledger**: one row per
line, into Available, carrying the receipt number as the document and the
clerk's name. That is how stock enters the system.

### A part-delivery is not a shortage

This is the step most worth getting right, and the one that reads oddly
until you have seen why.

Two different things can be wrong with a delivery, and from the warehouse
floor they look the same — sixty trousers came off the van:

* **The centre has not finished.** They sent 60 of 100 and the rest is still
  being sewn. Nothing is lost; the order simply has 40 to come.
* **The centre sent 100 and 60 arrived.** Forty went missing between the
  workshop and the warehouse, and somebody has to find out where.

The only thing that tells them apart is **what the Tailoring Centre's sheet
says it put on the van**. That is what the tick is for. Ticked, you are
saying the sheet and your count agree — so a 60 of 100 delivery is a
part-delivery, and the order reads 40 still outstanding. Unticked, you type
what the sheet claimed, and the gap is reported as a shortage for somebody
to chase.

> **Say this in training.** The tick is on by default because almost every
> delivery matches its sheet, and nobody should have to type the same number
> twice to say so. Untick it **only** when the paper and the van disagree.
> A clerk who unticks nothing is telling the system every sheet was right.

**The packing list number is free text and not unique.** It is a number
handwritten on a sheet of paper, and two Tailoring Centres may number their
own books independently without either being wrong.

**But the same number twice against one production order is refused.**
Posting a receipt raises stock, so keying one van in twice puts goods on the
shelf that never arrived — and because the ledger cannot be edited, undoing
it means a stock correction somebody has to notice is needed. The refusal
names the receipt that already holds the number, and spelling it differently
or in another case will not get past it.

**Short deliveries are expected.** The reason you give is kept on the receipt
and shown on the production order, so a shortage is a documented fact rather
than a mystery.

If a receipt is recorded but the posting fails, the production order shows it
as recorded and not posted, and there is an action on the receipt to post it.
That matters: a receipt with no stock behind it means the warehouse believes
goods are in when the system does not.

### Printing the receipt

The receipt is a document that gets signed and filed — the *Finalized Cargo
Receipt & Manifest*. It is produced twice over: once at the end of
recording, and again whenever anybody needs a copy.

**At the end of recording.** When the delivery is finalised the manifest is
shown straight away, with a **Print Receipt** button above it. That is the
sheet the warehouse signs and files.

**Afterwards, from the production order:**

1. Open the production order the delivery came in against.
2. Find the delivery in **Receipt History Logs**.
3. Click the receipt number — `RC-100004`.
4. **Print Receipt**.

What prints is the same document, not a copy made to look like it. On screen
that page is a plain summary — four facts and a table of what arrived
against what the packing list claimed. On paper it is the manifest, and the
screen's own headings, buttons and breadcrumbs are left off.

The manifest carries:

| | |
|---|---|
| Header | AsOne Logistics, the warehouse, and whether the receipt is **COMPLETED** or **NOT POSTED** |
| Meta | production order, warehouse, receipt date, who received it, packing list number, supplier (shipping TC), carrier, receipt number |
| Table | SKU, description, expected, received, variance, and a status of MATCHED, SHORTAGE or SURPLUS per line |
| Total | aggregate units expected and received, the net variance, and whether the delivery was CLEAN, NET SHORT, NET SURPLUS or OFFSETTING |
| Footer | whether inventory was updated, when it was posted, and a line for the warehouse lead's authorisation |

**A clerk sees their own warehouse's receipts only.** Opening one from
another site reports that it could not be loaded rather than showing the
goods.

**There is no list of receipts yet.** A receipt is reached through the
production order it came in against, or by its own address if you have it.
A screen answering "every delivery into Namayemba last month" is not built.

---

## 13. Inventory and stock corrections

**Inventory** shows what is on the shelf, by SKU and warehouse. The figures
are summed from the ledger every time the screen is opened.

When a physical count disagrees with the system, **Inv. Adjustments** is
where it is put right. This is a Finance screen — nobody else sees it.

Posting a correction:

1. Choose **Inventory Correction** as the type.
2. Pick the item and the warehouse.
3. The system shows what it thinks is there. You type the **physical count**.
4. The difference, the adjustment and the reason code are worked out for you
   — nobody counting has to do the subtraction or choose a direction.
5. Add a note saying where it was found, who counted it, which shelf.

Before you post, the screen states plainly what will happen: *"posting this
will reduce available inventory for UNI-HS-BPT-XS by 63 units at
Namayemba, immediately and permanently. Available becomes 7, and the change
is worth UGX 63,000."*

**Once posted it cannot be edited or deleted.** The 50 is not overwritten by
a 60 — a `+10` correction is added as its own row, and the level becomes 60
because the level is the sum of every row. A mistake is fixed by posting the
opposite entry.

**Use the notes box.** It is the only place the reason *behind* the reason
code is recorded, and it is what an auditor reads a year from now.

The other kinds of adjustment are **Return**, **Pick Up/Loss**, **Damaged**
and **Warehouse Transfer**, each with its own reason code and direction.

---

## 14. Stock history

The ledger itself: every movement in and out of every warehouse you can see,
newest first, with the document that caused it and the person who posted it.

It answers a different question from Adjustments. *"What did Finance change,
and why"* is the adjustments screen. *"Where did these 640 units go"* is this
one — and only this one can answer it, because it shows all eight movement
types rather than the one kind adjustments covers.

| Column | What it tells you |
|---|---|
| **Txn #** | The ledger's own number for this movement |
| **Movement** | Receipt, Pick, Shipment, Transfer in or out, Adjustment, Return, Damage |
| **Reason** | Why, for the movements raised *for* a reason. "Adjustment" covers a miscount, a breakage, a loss and a return — this is what tells them apart. A receipt or a pick shows a dash: those happened for a document, not a reason |
| **Stock** | Available, Picked or Shipped |
| **Qty** | Signed — positive came in, negative went out |
| **Document** | The paper behind it: `RC-`, `SH-`, `ADJ-`, `WT-`, `SO-` |
| **Posted by** | Who did it |

**Narrow to one SKU in one warehouse and a Balance column appears**, giving
the level after each movement — so a correction reads `150 → 155` rather than
just `+5`. It only shows under that filter, because a running total across
several items or several sites adds up quantities that were never in the same
pile.

The SKU filter is typed into rather than scrolled; typing `swt xs` matches on
both words in any order.

**Nothing here can be edited or deleted** by anybody, including through the
API. Stock levels are summed from these rows, so changing one would rewrite
history and today's figure at the same time.

**Click any row to open it.** Eleven columns still cannot carry everything a
movement holds — a transfer's source and destination, the exact unit and
total value, the moment it was *written* as against the day it happened, and
the level after the movement where that is known. Those are in the dialogue.

**Export CSV** takes the whole filtered ledger into a spreadsheet, not the
page on screen. Fifteen columns, including the three the table has no room
for: From, To and the document.

---

## 15. School orders, picking and shipping

This is Phase 3. The screens exist and the flow below is what they do.

**A school places an order** for a named student, choosing items at either
the **kit or the SKU level**. A kit is exploded into its component SKUs at
that moment.

The order starts on **hold**. An invoice is created with prices, carrying the
same number as the order. When payment is confirmed the order is **released**
to the warehouse — releasing *is* the payment confirmation; there is no
separate step.

**The warehouse picks**, which moves stock from Available to Picked. A pick
list is printed in description order, which is the order things sit on the
shelf.

**Shipping** sends the parcel to the school with a packing list showing what
is in it and who it is for. Shipments go out weekly.

**Picked and Shipped are different physical facts.** Picked means pulled off
the shelf and still in the building. Shipped means it has left. A parcel that
left three days ago is shipped but not yet complete — complete means the
school has confirmed it arrived.

The school uses the invoice number and the student's name to give the right
parcel to the right child. Students do not have accounts.

Two documents come off an order, and they are different papers:

| | What it is | Carries prices |
|---|---|---|
| **Invoice** | What a parent pays against and the school files. Available from the moment the order is placed | Yes |
| **Delivery slip** | What travels with the parcel and the school signs for | No |

Both are printed from the order. The invoice fills in the payment where the
system knows it — releasing an order *is* the payment confirmation, so a
released order prints the date and the reference rather than a blank line.
What stays blank is only what is still to happen: the signature taken when
the uniform is handed to the student.

---

## 16. Backorders and transfers

**Nobody creates a backorder.** There is no button and no record to tidy up
afterwards. A backorder is a *situation*: a paid order its warehouse cannot
fill. It stops being one the moment stock arrives or the order moves to a
warehouse that has the stock.

**An order is held whole.** If a warehouse cannot fill every line, nothing
ships. A school never receives a parcel with half a uniform in it — a child
cannot wear a shirt with no shorts, and deliveries are weekly, so
part-filling would mean a second delivery weeks later for one missing item.

Orders waiting for stock are released **oldest first**.

### Transferring an order to another warehouse

When a warehouse cannot fill an order, the clerk can hand it to one that can.

1. The clerk opens the waiting queue and sees exactly what the order is short
   of.
2. The system offers **only** warehouses holding enough of *every* line. The
   clerk never picks freely and cannot browse other warehouses' shelves.
3. The clerk transfers it, with a reason.
4. That warehouse picks and ships **straight to the school**.

Four things people get wrong about this:

- **No stock moves.** Nothing changes in inventory at either warehouse. What
  moves is responsibility. Stock moves later, when the new warehouse picks.
- **The goods do not route through the school's own warehouse.** They go from
  the shelf that had them, straight to the school.
- **The school's warehouse does not change.** Their next order still goes to
  their usual one. A transfer moves one order, never the relationship.
- **The order leaves the sending warehouse's screens**, which is correct — it
  is not their job any more.

A transfer is refused, with the reason on screen, when the receiving
warehouse cannot fill every line either, when it is already the one filling
it, when the order has not been paid for, or when it has already been picked
— stock is reserved, so it must be unpicked first.

---

## 17. Reports

Reports are grouped by what they answer.

| Report | What it shows |
|---|---|
| **Inventory** | What is on the shelf, by SKU and warehouse, with value |
| **Procurement costs** | What has been committed to the Tailoring Centres, by group order and production order |
| **Price list** | The current Primary and High School price lists, including kits |

The price list is the one report that matters before anything has moved: it
is what a school is quoted from, and it is pure master data.

---

---

*This is the reference edition, for the people who use and run the system.
Notes on the admin interface, on design decisions and on questions still
open with AsOne are kept with the project rather than here.*
