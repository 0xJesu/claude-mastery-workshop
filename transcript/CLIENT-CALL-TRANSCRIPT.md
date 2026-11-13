# Fictional Client Call Transcript: Tiffin Service Ordering App

**Claude Mastery Workshop, 14 Nov 2026 - Requirements Exercise**

> **This transcript is fictional.** It was written for a classroom exercise. The business, the people and every detail in it are invented, and it does not record a real call. Use it to practice turning a messy client conversation into requirements, a small spec and a working first slice.

*Setting: A consultant who builds small software for local businesses speaks with the owner of a tiffin (dabba) lunch delivery service. The call lasts about 20 minutes. Speakers: CONSULTANT and CUSTOMER (Meera, owner of "GharSe Tiffin", an invented business).*

---

**CONSULTANT:** Thanks for taking the call. Tell me how orders come in today.

**CUSTOMER:** Mostly phone calls. Some WhatsApp messages. Whoever is in the office writes it into a Google Sheet. Name, address, how many thalis, veg or non-veg.

**CONSULTANT:** Walk me through a normal morning.

**CUSTOMER:** Calls start around 8. We take orders for lunch the same day. By 10:30 or 11 the kitchen wants the final count, so we stop taking orders. Roughly.

**CONSULTANT:** Roughly?

**CUSTOMER:** (laughs) Officially 11. But if a regular calls at 11:20, my staff sometimes adds them anyway. Then the kitchen complains they cooked for 60 and we have 64 orders.

**CONSULTANT:** How many orders on a typical day?

**CUSTOMER:** Sixty to eighty. More on Mondays for some reason.

**CONSULTANT:** You mentioned the sheet. Any problems with it?

**CUSTOMER:** The same order goes in twice. Someone calls, my helper notes it, then the customer calls again to change something and someone else adds a new row instead of fixing the old one. We find out only when the customer gets two deliveries, or calls angrily at 2 pm.

**CONSULTANT:** How do you know which orders are actually confirmed?

**CUSTOMER:** That is the daily headache. The kitchen keeps asking me "what is confirmed?" and I am checking the sheet, then WhatsApp, then the call log. Sometimes an order marked confirmed in the sheet was cancelled on a call and nobody updated it.

**CONSULTANT:** What happens when someone cancels?

**CUSTOMER:** If they have paid in advance, we owe them money back. Right now my office boy writes "refund" in a notebook and sends it on UPI when he remembers. Customers keep calling again and again: "did you note my refund?" We have nothing we can show them.

**CONSULTANT:** If I built you something, what is the one thing it must do?

**CUSTOMER:** A small screen. My staff adds an order, and we can see its status. New, confirmed, cancelled. If a lunch is cancelled, staff should be able to record that a refund is requested, so when the customer calls back, anyone in the office can see it.

**CONSULTANT:** Who uses this screen?

**CUSTOMER:** The office staff. Two, maybe three people. Customers do not need to see it. Maybe later, not now.

**CONSULTANT:** Do refunds happen inside this screen too? The actual money?

**CUSTOMER:** No no, money we still send on UPI ourselves. I just want to know it was noted, and that nobody records the same refund twice. That has also happened. We paid a man twice last month.

**CONSULTANT:** What about payments when the order is placed?

**CUSTOMER:** Most customers pay monthly or on delivery. Advance payment is only for bulk orders. Do not build a payment gateway, I do not want that expense.

**CONSULTANT:** Would you want customers notified when their order is confirmed?

**CUSTOMER:** Would be nice. But not if it makes this complicated. First let the screen work.

**CONSULTANT:** Anything else that goes wrong?

**CUSTOMER:** Special cases. A company calls at 11:45 wanting 20 thalis for a meeting, and it is important, so we take it. I do not want software that blocks us from being flexible.

**CONSULTANT:** What does success look like in three months?

**CUSTOMER:** Less manual checking. Fewer angry calls. I do not want a huge new system that my staff refuses to use. If it saves my office one hour a day, I am happy.

**CONSULTANT:** Last one. If two of your staff add the same order at the same time, what should happen?

**CUSTOMER:** It should not become two orders. Obviously. How you manage that is your job, not mine. (laughs)

*End of transcript.*

---

## For participants

Work in pairs. Before writing any code, pull out of this transcript: (1) the stated needs, (2) the assumptions you are making, (3) the questions only the customer can answer, and (4) what is clearly out of scope. Notice what the customer never pinned down: the exact cutoff rule, what counts as a duplicate, who approves a refund, and how "special cases" should actually behave. Ask your instructor, who plays the customer, before you lock your spec.
