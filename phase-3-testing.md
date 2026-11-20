# Phase 3: what to test, and what you should see

Phase 3 is the outbound half of the system. A school orders a uniform for a
named student, the parent pays, the warehouse picks and ships it, and the
school confirms the parcel arrived. Everything before this phase put stock on
a shelf. This is how it reaches a child.

This page lists every Phase 3 feature, the steps to try it, and what you
should see if it is working. Work down the page in order: later tests use
the order you created in the earlier ones.

Each feature carries its number from the requirements pack, so a note you
send back can say "F39 failed" and we will know exactly what you mean.

**Where to find the system.** Open
**https://logistics.asoneministries.org** in Chrome, Edge or Safari.

---

## Before you start

**Four sign-ins.** Most of these tests change role halfway through. Open each
one in a separate browser window or profile so you are not signing in and out
on every step.

| Role | Used for |
|---|---|
| School Staff | Placing orders, paying, confirming delivery |
| Warehouse Staff | Picking, packing, despatch, transfers |
| Finance Department | Invoices, the costed reports |
| Program Lead or Operations Manager | The queues and reports across every site |

**Stock on the shelf.** Picking fails when the warehouse is short, which is
correct and is its own test further down. For the first half of this page you
need a warehouse that actually holds the garments you order. Check under
**Inventory** before you begin.

**Two schools, two warehouses.** The transfer tests need a second warehouse
holding stock that the first one does not. Without it the transfer screen has
nothing to offer and the test proves nothing.

**If a step fails**, write down the order number, the screen you were on, the
time, and what you saw instead. The order number is the single most useful
thing in that list.

---

## The school's half

### F29. A school orders from its own price list

**Who:** School Staff at a Primary school.

| Step | What you should see |
|---|---|
| 1. Orders, then **Place order**. | The new order form opens. |
| 2. Under **Individual items**, click **Add an item** and open the picker. | Only Primary School garments are listed. Nursery and High School items are not there at all. |
| 3. Choose any item. | A price appears in the **Each** column, and the foot of the form reads **Estimate at today's prices**. |
| 4. Set **Order date** to a date before the last price change, place the order, then print the invoice. | The invoice is priced at the figure that was in force on the order date, not today's. |

The point of the test is the absence: a Primary school cannot reach a High
School garment even by accident, because the list is built from the school on
your own account.

Step 4 is why the figure on the form says **Estimate**. The picker always
shows today's prices; the order is costed on the date you set, when you place
it. If the two differ, the invoice is the one that is right.

### F30. Kits and individual items on one order

**Who:** School Staff.

| Step | What you should see |
|---|---|
| 1. On the same form, click **Add a kit** and pick a kit. | The kit is added as one line with a quantity. |
| 2. Click **Add an item** and add a single garment as well. | Both tables now have a line. The two are kept separate on purpose. |
| 3. Set a quantity on each. | The foot of the form says how many items on how many lines, with an estimate beside it. |

A school may order a whole kit, loose garments, or both on the same order.
All three must work.

### F31. The order is for a named student

**Who:** School Staff.

| Step | What you should see |
|---|---|
| 1. Leave **Student** empty. | The foot of the form reads **Who is this order for?** and **Place order** is greyed out. |
| 2. Type a student's name. | The prompt is replaced by the line count, and the button becomes clickable. |
| 3. Remove every line instead. | The prompt becomes **Add a kit or an item.** and the button greys out again. |

Students have no accounts and no records of their own. The name is free text,
which is AsOne's own decision, and it is how the school hands the right
uniform to the right child when the parcel arrives.

### F32. A new order is on hold

**Who:** School Staff.

| Step | What you should see |
|---|---|
| 1. Click **Place order**. | You are taken to the new order. Note its number. |
| 2. Look at the status on the order. | **On hold, awaiting payment**. |
| 3. Open **Shipments** as Warehouse Staff and look at the picking backlog. | The order is not there. |

Nothing reaches the warehouse until the money is confirmed. If a brand new
order appears in the warehouse queue, that is a failure.

### F33. A kit becomes the garments inside it

**Who:** School Staff, on the order you just placed.

| Step | What you should see |
|---|---|
| 1. Scroll to the lines on the order. | The kit has broken apart into its individual garments, each with its own quantity and price. |
| 2. Look for the kit's own number beside those lines. | Each line says which kit it came out of. |

A kit is not stock and never sits on a shelf. The warehouse picks shirts and
shorts, so the order has to say shirts and shorts. The school still sees the
kit it bought on the invoice, which is the next test.

### F34. The invoice the school hands to the parent

**Who:** School Staff, or Finance for any school.

| Step | What you should see |
|---|---|
| 1. On the order, click **Print Invoice**. | Your browser's print preview opens. |
| 2. Read the number at the top. | It is the same number as the order. There is no separate invoice series. |
| 3. Look at the kit lines. | They are grouped back under the kit, with a subtotal, not scattered as loose garments. |
| 4. Look at the heading row of the table, and the rule under the word INVOICE. | Both carry AsOne's green. |
| 5. Look at the foot of the sheet. | Blank lines for **Paid**, **Received by** and **Date**, because none of it has happened yet. |

If the heading row prints white on white, say so: it means your browser or
printer is set to drop background colours, and we need to know which one.

### F35. Confirming payment releases the order

**Who:** School Staff only. Nobody else can do this.

| Step | What you should see |
|---|---|
| 1. On the order, find **Fulfillment Queue Control**. | A **Payment reference** box and a **Release for Picking** button. |
| 2. Leave the reference empty. | The button is greyed out. |
| 3. Type the receipt number from the payment system, for example RCT-2026-00841. | The button becomes clickable. |
| 4. Click **Release for Picking**. | The status changes to **Released to the warehouse**, and the reference is printed beside the release date. |
| 5. Sign in as Warehouse Staff and open **Shipments**. | The order is now in the picking backlog. |
| 6. Sign in as Finance and open the same order. | There is no release button. Finance cannot release an order. |

Releasing **is** the payment confirmation. There is no separate step. The
reference cannot be added afterwards, which is deliberate: an order released
without one could never be matched to the money.

### F36. Cancelling an unpaid order

**Who:** School Staff only.

| Step | What you should see |
|---|---|
| 1. Place a second order and leave it on hold. | Status **On hold, awaiting payment**. |
| 2. Click **Cancel Order**. | You are asked to confirm, and asked for a reason. |
| 3. Confirm. | The status becomes **Cancelled**, and who cancelled it, when, and why are all recorded on the order. |
| 4. Open the order you released in F35 and look for the same button. | It is gone. A released order cannot be cancelled. |
| 5. Look for a way to delete either order. | There is none, anywhere. |

An order is withdrawn, never deleted. The school has already handed that
number to a parent on a piece of paper, so the document has to survive.

---

## The warehouse's half

Switch to **Warehouse Staff** for everything in this section.

### F37. What the warehouse can and cannot fill

**Who:** Warehouse Staff, or a lead.

| Step | What you should see |
|---|---|
| 1. Open **Shipments**. | The **To Pick** tab, with the picking backlog below it. |
| 2. Find the order released in F35. | It is listed, with the school, the student and how many items. |
| 3. Check the stock figures under **Inventory** for one of its garments. | Nothing has moved. Looking at an order reserves nothing. |

The warehouse only ever sees orders for its own site. If you can see another
warehouse's order here, that is a failure worth reporting immediately.

### F38. The pick list: built, and switched off for now

**Nothing to test here.** Turned off at your request on 20 November 2026.

| Step | What you should see |
|---|---|
| 1. Open a released order as Warehouse Staff. | **Print Invoice** and **Print Packing List**. No **Print Pick List**. |

Only the button is hidden. The sheet itself, and everything behind it, is
built and in place, so turning it back on is one line and no rebuild of the
feature. If you want it back during testing, say so.

What it does, for when that decision comes back around. It is the sheet a
clerk carries to the shelf: the garments and quantities with a box to tick
per line, the student and the warehouse at the top, one signature rule for
**Picked by**, and nothing about a van or a carrier, because none of that
has happened yet. A garment that appears both inside a kit and on its own
is one line with the total, so nobody walks the same aisle twice.

It exists as a second document because a packing list printed before
despatch has nothing to put in half its fields, which is the wrong sheet to
hand somebody walking to a shelf. With it hidden, the packing list is doing
both jobs, and F40 step 5 is what that costs.

### F39. Picking reserves the stock

**Who:** Warehouse Staff.

| Step | What you should see |
|---|---|
| 1. Open **Inventory**, click one of the garments on the order, and write down **Available** and **To Pick** from the panel that opens. | Both figures are shown under STOCK SUMMARY. |
| 2. Back on the picking backlog, click **Start Pick** on the order. | You are asked to confirm, and told how many items it reserves and for whom. |
| 3. Confirm. | The button becomes a spent **Picked** button and stays on the row. |
| 4. Open the same garment in **Inventory** again. | Available has dropped by the picked quantity. **To Pick** has risen by the same amount. The total in the building has not changed. |
| 5. Open the order. | Status **Picked**, and an **Undo Pick** button has appeared. |
| 6. Click **Undo Pick**, give a reason, then check the garment again. | The figures are back where they started, and the order is back in the picking queue. Both entries stay in the stock history. |
| 7. Pick it again before carrying on. | Status **Picked**. |

Now the test that matters most:

| Step | What you should see |
|---|---|
| 8. Place and release another order for more of a garment than the warehouse holds. | It is accepted. The school's half does not depend on stock. |
| 9. Try to pick it. | It is refused, and nothing is reserved. Not one line of it. |

An order is picked whole or not at all. A school never receives half a
uniform: a child cannot wear a shirt with no shorts, and deliveries are
weekly, so part filling would mean a second delivery weeks later for one
missing garment.

### F40. The packing list that travels with the goods

**Who:** Warehouse Staff.

| Step | What you should see |
|---|---|
| 1. On the picked order, click **Print Packing List**. | A sheet headed **Packing List**, in the design AsOne sent us. |
| 2. Check the items. | Only the items on **this** order, for **this** student. Nobody else's child appears. |
| 3. Check the heading row of the table. | AsOne's green, white text. |
| 4. Check the two address blocks. | **From (Sender)** is the warehouse it is leaving, **To (Consignee)** is the school it is going to, both with their addresses. |
| 5. Check **Ship Date** and **Carrier Method**. | **Not yet shipped** and **Not yet assigned**, because the order has been picked but no van has gone. The sheet says so rather than printing a blank. |
| 6. Look at the foot. | Two signature rules, **Packed by** and **Received by**, and the totals. |
| 7. After F41, despatch it and print the packing list again. | Both fields are now filled in, and so is the waybill number. |

Step 2 is the one to be fussy about. This is the fault reported on
20 November 2026, when a one item order printed four children's garments.
Print the packing list for every order on a consolidated van and check each
one names a single child.

Steps 5 and 7 are why the pick list was built as a separate sheet. With it
switched off, this is the only sheet available before despatch, so a clerk
picking from it is reading a document that says **Not yet shipped** and
**Not yet assigned** and carries a consignee block and two signature rules
for a parcel that does not exist yet. That is workable, and it is worth
knowing it is the trade being made. See F38.

### F41. Despatch, and the school confirming the parcel

**Who:** Warehouse Staff, then School Staff.

| Step | What you should see |
|---|---|
| 1. On **Shipments**, find **Ready to Despatch**. | The school is listed, with how many orders are waiting for a van. |
| 2. Click **Despatch**. | You are warned that stock leaves the warehouse and it cannot be undone. |
| 3. Confirm. | A shipment is created. Note its number. |
| 4. Open the garment in **Inventory**. | **To Pick** has dropped and **Shipped** has risen by the same amount. The stock has left the building. |
| 5. Open the order. | Status **Shipped**. |
| 6. Sign in as School Staff and open the same order. | A **Confirm Delivery Received** button, and a box for anything wrong. |
| 7. Click it. | Status becomes **Received by the school**. |
| 8. Before step 7, look at the same order as Warehouse Staff. | No button, just **In transit. The order completes when the school confirms it arrived.** A warehouse cannot confirm its own delivery arrived. |

Shipped and Received are deliberately different facts. Everything sitting in
the gap between them is a parcel somebody should be chasing. Without the
distinction, a delivery that never turned up looks exactly like one that did.

### F42. One van, one school, every order that is ready

**Who:** Warehouse Staff.

| Step | What you should see |
|---|---|
| 1. Place, release and pick **three** orders for the same school, for three different students. | All three sit at **Picked**. |
| 2. Open **Ready to Despatch**. | One row for that school, saying three orders. Not three rows. |
| 3. Despatch, and open the shipment. | One shipment carrying all three orders, with every student named on it. |
| 4. Open **one** of the three orders and print its packing list. | That child's garments only. |
| 5. Open the shipment itself. | Every child on the van, which is what the school needs to distribute them. |

Same despatch, two different questions. Step 4 and step 5 should **not**
show the same thing.

---

## When a warehouse cannot fill an order

Nobody creates a backorder, and there is no button for one. A backorder is a
situation: a paid order its warehouse cannot fill. It stops being one the
moment stock arrives, or the order moves to a warehouse that has the stock.

### F43. Orders waiting for stock

**Who:** Warehouse Staff, or a lead.

| Step | What you should see |
|---|---|
| 1. Place and release an order the warehouse cannot fill. | It is accepted. The school's half does not depend on stock. |
| 2. Open **Backorders** in the menu. | The order is listed, with the school, the day it was placed, and what it is waiting on. |
| 3. Look at the **Waiting on** column. | The garments it is short of, with quantities. |
| 4. Look at the order of the rows. | Oldest first. Orders waiting for stock are released in the order they were placed. |
| 5. Open the bell at the top of the screen. | An alert saying how many school orders are waiting for stock. |
| 6. Click the alert. | It takes you to the Backorders screen. |

Step 5 is new, added on 20 November 2026. The school was always told its
items were on backorder; the warehouse, the only party that can do anything
about it, was told nothing.

### F44. What the school is still owed

**Who:** School Staff, on their own dashboard.

| Step | What you should see |
|---|---|
| 1. Sign in as the school whose order is waiting. | The school dashboard. |
| 2. Find the **Backordered** tile. | A count, and it is highlighted rather than plain. |
| 3. Read the list below it. | Each garment the school is still owed, with its quantity. |
| 4. Check the label on each. | **UNASSIGNED**, meaning nobody has taken it on yet. |
| 5. Transfer the order, as in F45, then look again. | The garments are gone from the list, because a warehouse that has the stock now holds the order. |

This is the answer to "where is my child's shirt". The list is worked out
from what the warehouse is short of at that moment, so nothing has to be
marked resolved by hand and the school's screen cannot disagree with the
warehouse's.

The second label, **BEING FILLED**, belongs to part shipping, which is
switched off pending the decision at the foot of this page. You will not see
it, and that is correct for now.

### F45. Transferring the order to a warehouse that has the stock

**Who:** Warehouse Staff, or a lead.

| Step | What you should see |
|---|---|
| 1. On **Backorders**, click **Transfer** on a waiting order. | A window headed **Transfer**, naming the order, the school and the warehouse it is at now. |
| 2. Open **Transfer to**. | Only warehouses that hold enough of **every** line are offered. A warehouse that could fill half of it is not on the list. |
| 3. Pick one, type a reason, and click **Transfer the order**. | The order leaves the Backorders screen. |
| 4. Check **Inventory** at both warehouses. | Nothing moved. Not a single garment. |
| 5. Sign in as the sending warehouse and look at its queues. | The order is gone from all of them. |
| 6. Sign in as the receiving warehouse and open **Shipments**. | The order is in its picking backlog. |

What moves is responsibility, not stock. The receiving warehouse picks in the
ordinary way afterwards, and that pick is what finally touches inventory.

If no warehouse can fill it on the day, the list in step 2 is empty and the
window says so. That is correct behaviour, not a fault, but it makes a poor
test: receive stock into the second warehouse first.

### F46. The filling warehouse ships straight to the school

**Who:** Warehouse Staff at the receiving warehouse.

| Step | What you should see |
|---|---|
| 1. Pick and despatch the transferred order. | A shipment, as usual. |
| 2. Open the shipment and read where it is going. | Straight to the school. Not back through the school's own warehouse. |
| 3. Print its packing list. | The sending warehouse is the one that actually holds the stock, not the school's own. |
| 4. Open the school's record and check its warehouse. | Unchanged. |

A transfer moves one order. It never moves the relationship between a school
and its warehouse.

---

## The reports

### F53. Invoices raised but not yet paid

**Who:** Finance, a lead, or a school for its own orders.

| Step | What you should see |
|---|---|
| 1. Open **Orders** and set **Status** to **On hold, awaiting payment**. | Only orders still waiting for payment, with the student, the total and the date. |
| 2. Sign in as a school and look at the same list. | That school's orders only. |
| 3. Sign in as Finance or a lead. | Every school's orders. |
| 4. Check the order of the rows. | Newest first, which is the order every list in the system uses. |

**One thing to decide.** The requirement asks for the longest unpaid invoice
first, and the system can already answer that way, but this screen is the
ordinary orders list with a filter on it rather than a report of its own. So
the oldest sits at the bottom. If Finance would rather have a chasing list
that puts the oldest at the top, say so and we will build it as a report.

### F52 and F54. Picked but not yet despatched

**Who:** Warehouse Staff, or a lead.

| Step | What you should see |
|---|---|
| 1. Open **Shipments**. | Three tiles: Ready to Pick, Picked, Completed Today. |
| 2. Read the **Picked** tile. | How many orders are reserved and waiting for a van. |
| 3. Read **Ready to Despatch** below it. | The same orders, grouped by the school they are going to. |
| 4. Despatch one school's orders and read the tile again. | The count has dropped by that school's orders. |

This is the gap between a pick list being generated and a packing list being
created, which is the report AsOne asked for twice on page 9.

### F49. Backorders outstanding

**Who:** Warehouse Staff, or a lead.

| Step | What you should see |
|---|---|
| 1. Open **Dashboard**. | A **Backorders** tile reading **Orders waiting for stock**, with a count on it. |
| 2. Open **Backorders**. | The same number of orders listed. |
| 3. Fill one, by receiving stock or by transferring it. | Both the tile and the list drop by one, with nothing marked resolved by hand. |

Step 1 changed on 20 November 2026 and is worth checking carefully. The tile
used to count a stored table that nothing writes to while orders are held
whole, so it read zero on a database with three orders sitting on the
Backorders screen. It now counts the same orders the screen lists, which is
the only number worth putting on a tile that leads to it.

### F57. What each school received, and what it was worth

**Who:** Finance, or a lead.

| Step | What you should see |
|---|---|
| 1. Open **Reports** and find the **Sales & Schools Reports** card. | **Shipments to Schools** is listed, and its title is a link. |
| 2. Click it. | One row per school: shipments, units and value. |
| 3. Set a From and To date. | The figures narrow to that range. |
| 4. Click the export button. | A spreadsheet downloads with the same rows. |
| 5. Compare the value with the stock reports. | They do not agree, and are not meant to. |

Step 5 is worth understanding before you query it. This report values a
shipment at **what the school was charged**, taken from the order on the day
it was placed. The stock reports value the same garments at **what they cost
the warehouse**. Two honest answers to two different questions.

---

## Two things we need a decision on

Neither blocks testing. Both change what gets built next.

**Partial shipping.** Page 8 of the pack says an order is held until it can
be filled, and that is what F39 does. The note of 24 August also mentions
transferring backorders, which could be read as shipping an order in parts.
We built the first reading and left the second switched off. If an order
should be able to ship in halves, tell us and we will turn it on.

**The Colour column.** The packing list design has one. Colour was removed
from the catalogue on 23 October at your request, on the basis that the
garment names carry it, such as Grey Shorts and Navy T-Shirt. There is
currently nothing to print in that column, so it is left out rather than
printed empty on every row. Putting it back is a catalogue change, so we are
raising it rather than deciding it.

---

## Words you will see on these screens

| Word | What it means here |
|---|---|
| **On hold** | Ordered, invoiced, not yet paid. The warehouse cannot see it. |
| **Released** | Paid for. The warehouse can now act on it. |
| **Picked** | Pulled off the shelf and reserved. Still in the building. |
| **Shipped** | It left the warehouse. |
| **Received by the school** | The school confirmed the parcel arrived. |
| **Cancelled** | Withdrawn before payment. The record stays. |
| **Backorder** | A paid order its warehouse cannot fill. Not a record, a situation. |
| **Transfer** | Handing an order to a warehouse that has the stock. No stock moves. |
| **Pick list** | The sheet you carry to the shelf. Built, switched off for now. |
| **Packing list** | The sheet that travels with the parcel. |
