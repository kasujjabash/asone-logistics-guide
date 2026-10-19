# Using the AsOne Logistics system

How to do each job, step by step.

This is written for the people who use the system to do their work — raising
orders, receiving deliveries, checking stock. Nothing in it is technical, and
you do not need to read it end to end: find your job in the list and follow
the steps in order.

Keep this page open while you work. It is the same for everyone, so if a
colleague describes a screen differently, you are both looking at this.

**Where to find the system.** Open **https://logistics.asoneafrica.org** in
your web browser — Chrome, Edge or Safari. There is nothing to install.

---

## Contents

| | |
|---|---|
| [Signing in](#signing-in) | Your first time, and your password |
| [The menu down the left](#the-menu-down-the-left) | What each item is for |
| [Job 1](#job-1--create-a-production-order) | Create a production order |
| [Job 1b](#job-1b--import-many-production-orders-from-a-spreadsheet) | Import many orders from a spreadsheet |
| [Job 2](#job-2--receive-a-delivery-from-a-tailoring-centre) | Receive a delivery |
| [Job 3](#job-3--when-an-order-arrives-in-two-deliveries) | When an order arrives in two deliveries |
| [Job 4](#job-4--find-and-print-a-receipt) | Find and print a receipt |
| [Job 5](#job-5--check-what-a-warehouse-holds) | Check what a warehouse holds |
| [Words the system uses](#words-the-system-uses) | Plain English for what is on screen |
| [If something goes wrong](#if-something-goes-wrong) | The red messages, and what to do |

---

## Signing in

1. Open the system in your web browser.
2. Type your email address and your password.
3. Click **Sign in**.

First time in, you are asked to set a new password. Choose one only you know.

## The menu down the left

Everything starts from the dark menu on the left of the screen.

| Menu item | What it is for |
|---|---|
| **Dashboard** | The first page. A summary of what is happening. |
| **Production Orders** | Orders placed on a Tailoring Centre. |
| **Receiving** | Recording goods that have just arrived at the warehouse. |
| **Receipts** | Deliveries already recorded. |
| **Inventory** | How much of each garment each warehouse holds. |

If you are warehouse staff, **Operations** opens and closes — the rest sit
beneath it and are always there.

If a menu item is not on your screen, your job does not need it. That is
normal and nothing is wrong.

## Job 1 — Create a production order

This is how you tell a Tailoring Centre what to make and where to send it.

1. Click **Production Orders** in the menu on the left.
2. Click the green **Create Production Order** button at the top right.
3. Under **Tailoring Center**, choose the centre that will make the garments.
4. Under **Destination Warehouse**, choose the warehouse they should be
   delivered to.
5. **Order Date** is already filled with today's date. Leave it unless the
   order was agreed on an earlier day.
6. Under **Required By**, pick the date the garments are needed in the
   warehouse. Leave it empty if no date has been agreed.
7. **Notes** is optional. Write anything the centre should know — it prints
   on the manifest they receive.
8. On the right, under **Garments Ordered**, click *Choose a garment…* and
   pick the first garment.
9. In the **Quantity** box next to it, type how many.
10. Leave **Agreed Price** empty unless a different price was agreed with
    that centre. Empty means the normal price list is used.
11. To add another garment, click **+ Add Garment** and repeat steps 8–10.
12. When every garment is listed, click **Create Order** at the bottom right.

The order opens on its own page with a number such as **PO-100024**. That is
the number to write on paperwork and give to the Tailoring Centre.

> **If Create Order is grey and will not click**, something is not finished.
> The grey bar at the bottom says what — usually a garment with no quantity,
> or no garment chosen.

## Job 1b — Import many production orders from a spreadsheet

Use this when orders already exist on paper and there are too many to type —
the 2027 orders the Tailoring Centres are already working from.

1. Click **Production Orders** in the menu on the left.
2. Click the small **arrow** at the right-hand end of the green
   **Create Production Order** button.
3. Choose **Import production orders…**
4. Click **Choose File** and pick the spreadsheet.
5. Click **Step 1 — check file**.
6. Read what comes back. It lists every order the file would create, with
   its centre, destination and how many garments. **Nothing has been saved
   at this point.**
7. If it looks right, click **Yes, raise these N orders**.

The orders now appear in the list, each with its own number.

**What the spreadsheet needs.** One row per garment. A **reference** column
saying which order each row belongs to, plus **Tailoring Centre**,
**Destination Warehouse**, **SKU** and **Ordered Quantity**. **Required By**
is optional. Rows sharing a reference become one order, so the centre,
warehouse and date must be the same on all of them.

> **Step 1 does not save anything.** It reads the whole file and tells you
> what would happen. The orders only exist after you press the second
> button. If you close the window after step 1, nothing has changed.

> **If it refuses the file**, it lists every problem at once with the
> spreadsheet row number. Fix them all, then check the file again. The
> commonest is a SKU the catalogue does not hold, which means the garments
> have not been imported yet.

**Imported orders show as *Awaiting delivery*.** That is correct — the
system works out delivery from receipts, and an imported order has none
yet. If the garments already arrived before the system went live, record
those deliveries with **Job 2** and the status corrects itself.

## Job 2 — Receive a delivery from a Tailoring Centre

Do this when a vehicle arrives and the garments have been counted. You need
the **paper packing list** the driver brings.

The screen walks you through four steps, shown along the top: **Select PO**,
**Packing List**, **Compare**, **Confirm**.

**Step one — say what arrived against what**

1. Click **Receiving** in the menu on the left.
2. Under **Select Production Order**, choose the order this delivery is
   against. It reads like *PO-100016 — Rwanyabihuka*.
3. In **Packing List Number**, type the number on the driver's paper, exactly
   as written.
4. In **Date Received**, pick the day the goods actually arrived.
5. In **Carrier / Driver Name**, type who delivered it.
6. Click **Save & Continue to Compare**.

**Step two — count the garments in**

You now see a row for each garment on the order.

| Column | What to do with it |
|---|---|
| **Ordered** | What was asked for. Nothing to do. |
| **Received (In)** | Type the number you physically counted. It starts **empty** — the system never guesses what arrived. A box with a dashed edge is one nobody has counted yet. |
| **As per packing list** | Leave the tick alone if the paper agrees with your count. Untick it and type the paper's number if they differ. |
| **Diff** | Worked out for you. |
| **Status** | Worked out for you. |
| **Reason** | Fill in only when the Status is not *Complete*. |

7. Go down the list and type what you counted into **Received (In)**.
8. If the paper says a different number from your count, untick **As per
   packing list** on that row and type the paper's number.
9. Click **Confirm & Finalize Receipt**.

The stock is added to the warehouse at that moment, and the delivery appears
under **Receipts**.

**Read the coloured line before you finalise.** On the right, above the
figures, one sentence says what kind of delivery this is:

| | What it means |
|---|---|
| 🟢 **Order complete** | Everything the order asked for has now arrived. |
| 🟡 **Part delivery** | Your count matches the paper. The rest is still being made and stays outstanding. **Not a problem.** |
| 🔴 **Shortage** | Fewer garments arrived than the paper said were sent. Say what happened in the notes. |
| 🔴 **More than declared** | More arrived than the paper declares. Check the count and the paper, and say what was agreed. |

Both red ones mean your count and the driver's paper disagree. Settle it with
him before he leaves — that is what the **Reconciliation Notes** box on the
right is for, and anyone opening the receipt later will read what you wrote.

## Job 3 — When an order arrives in two deliveries

A centre may send 60 garments this week and the other 40 next week. That is
normal. Record each delivery on its own: do **Job 2** again, with two things
to watch.

- Choose the **same production order**. The system remembers what already
  came in and shows what is still owed.
- Use the **packing list number from the new paper**. If you type one already
  recorded against that order, the system refuses it and says when the first
  was recorded — recording the same delivery twice would double the stock.

> **A part-delivery is not a shortage.** If 60 arrived and 60 were on the
> paper, that is a complete delivery of what was sent. The order still shows
> 40 outstanding because 40 are still being made. A shortage is different:
> fewer arrived than the paper said were sent.

## Job 4 — Find and print a receipt

1. Click **Receipts** in the menu on the left. Newest first.
2. Narrow the list with **Tailoring Centre** or **Status** at the top.
3. Click the receipt. You see what was expected, what arrived, and any
   difference.
4. Click **Print** at the top right, then print it or save it as a PDF.

To find a delivery when you only know the order, open **Production Orders**,
click the order, and its deliveries are listed on its page.

## Job 5 — Check what a warehouse holds

1. Click **Inventory** in the menu on the left.
2. Each row is one garment in one warehouse. **Available** is what is free
   to use.
3. Tick **Low Stock Only** to see just the garments running down.
4. Click **Export CSV** to open the figures in Excel.

The figures are worked out from every delivery and every issue recorded.
Nobody types a stock figure in by hand, which is why recording receipts
properly matters.

## Words the system uses

| Word on screen | What it means |
|---|---|
| **Production Order** | An instruction to one Tailoring Centre to make garments for one warehouse. Numbered PO-100024. |
| **SKU** | One exact garment: the item, its size and its colour together. A white shirt size XS is a different SKU from size S. |
| **Ordered** | How many were asked for. |
| **Received** | How many you counted in. |
| **Outstanding** | Ordered, less what has arrived. What is still owed. |
| **Shortage** | Fewer garments arrived than the paper said were sent. Something went missing. |
| **Part delivery** | The centre sent some now and will send the rest later. Not a problem. |
| **More than declared** | More garments arrived than the packing list says were sent. The paperwork and the van disagree. |
| **Packing list** | The paper the driver brings, listing what was loaded. |
| **Receipt** | The record of one delivery arriving. |
| **Posted** | The receipt is finalised and the stock has been added. |
| **Available** | Stock free to use, not already promised to a school. |
| **Agreed Price** | A price negotiated with a centre. Leave empty to use the price list. |

## If something goes wrong

A red message means the system refused to save and **nothing was changed**.
Read it — it says what to do.

| What you see | What to do |
|---|---|
| *Packing list … was already recorded against …* | That delivery is already in the system. Check the paper. If this really is a second delivery, use its own packing list number. |
| *The order was not created.* | The sentence after it says why. Fix that and click Create Order again. |
| A button is grey and will not click | Something is not filled in. The grey bar near the button says what. |
| *Everything on this order has already been received* | Nothing is owed on that order. Check you picked the right one. |
| *… is not in the catalogue* (on an import) | The garments have not been imported yet, or the SKU is mistyped. Fix the spreadsheet and check the file again. |
| You are sent back to the sign-in screen | Your session timed out. Sign in again; nothing you saved is lost. |

> **Nothing you record is ever deleted.** If you record a wrong figure, do
> not record it again — tell your supervisor, and a correction is made that
> keeps both the mistake and the fix on record.

**If you are stuck**, write down the production order number, the packing
list number and what the screen said. Those three things are enough to find
the problem.
