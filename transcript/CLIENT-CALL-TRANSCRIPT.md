# Fictional Client Call Transcript: Food-Ordering E-Commerce App

**Claude Mastery Workshop, 14 Nov 2026 - Requirements Exercise**

> **This transcript is fictional.** It was written for a classroom exercise. The business, the people and every detail in it are invented, and it does not record a real call. Use it to practice turning a messy client conversation into requirements, a small spec and a working first slice.

*Setting: A developer who builds small software for local businesses cold-calls the owner of a small restaurant in Karol Bagh, Delhi. They have never spoken before. The call lasts about 15 minutes. Speakers: JESU (the developer) and PRANJAL (owner of "Deka's Kitchen", an invented business).*

---

## Transcript

**JESU:** Hello, is this Pranjal Deka? Deka's Kitchen, Karol Bagh?

**PRANJAL:** Yes, speaking. Who is this?

**JESU:** Hi Pranjal, my name is Jesu. I'm a software developer. I picked up dinner from your counter last week - the chicken biryani - and took your number off the menu card. I build small online ordering websites for local kitchens. That's why I'm calling. Do you have five minutes, or is this a bad time?

**PRANJAL:** (laughs) The biryani was good, I hope. Lunch rush just ended, so five minutes is fine. What kind of website?

**JESU:** The simple kind. Your customer opens a link, sees your menu, picks what they want, and places the order themselves. It lands in one system on your side. Before I say more, can I ask - how do orders come in today?

**PRANJAL:** Phone calls. Mostly phone calls, some WhatsApp messages. My guy writes them in a register, then at the end of the day someone copies everything into an Excel sheet. Yesterday we found the same order entered twice - one from the register, one from the WhatsApp message. The customer got two thalis and paid for one. (laughs) He was happy. I was not.

**JESU:** (laughs) Okay, so duplicates are a real problem, not a theory. And someone on your team is doing the same data-entry twice, every single day.

**PRANJAL:** Exactly. It's a waste. But listen - I don't want Zomato. They take too much commission.

**JESU:** Good, because I'm not offering that. No listings, no ratings, no commission page. Just YOUR kitchen, YOUR menu, YOUR orders. One shop, online. You put the link on your WhatsApp status and on the menu card.

**PRANJAL:** Okay. That I would actually use. What would it look like from my side?

**JESU:** That's the right question. First walk me through the menu - how many items are we talking?

**PRANJAL:** Around 25-30 items. Veg thali 120, chicken thali 180, momos 80 a plate, chicken biryani 200, chowmein 90. A few combos on weekends. Prices change maybe once in two-three months. I should be able to edit the menu myself - mark something "not available today" when it runs out. That happens with biryani almost every Sunday.

**JESU:** So a menu you can edit yourself, with an available/not-available switch. Noted. Now after the customer places an order - what should happen on your side?

**PRANJAL:** My kitchen should see it immediately - new order, items, quantity, customer name, phone, address. Then we mark it: preparing, then out for delivery, then delivered. And the customer should be able to check the status themselves instead of calling me five times. "Where is my order?" - I get this twenty times a day.

**JESU:** Let me play it back: browse the menu, cart, place order, customer checks the status, and a simple kitchen screen moves each order along. One system, no register, no Excel.

**PRANJAL:** Yes. That's exactly it.

**JESU:** Now let me tell you what I will NOT build in the first version, and you tell me if that's okay.

**PRANJAL:** Go ahead.

**JESU:** One - no online payment. No UPI gateway, no card. Cash on delivery only. Payment gateways need documents, verification, and they take a cut. We can add it later.

**PRANJAL:** Fine. Most of my customers pay cash anyway.

**JESU:** Two - no delivery tracking on a map. No rider locations, no live GPS. Your delivery boy is not getting tracked.

**PRANJAL:** (laughs) He's my nephew, he would quit. Okay, no maps.

**JESU:** Three - no app to install. It's a website, a link. Your customers don't download anything, and you don't maintain anything.

**PRANJAL:** Even better. Half my customers have full phone storage anyway. Okay, I'm interested - what will this cost me?

**JESU:** First let me earn it. I'll write up what we discussed as a one-page requirements note and send it tomorrow. You read it, correct whatever I got wrong. Once you say "yes, this is exactly it", we talk money. If the note is wrong, you owe me nothing.

**PRANJAL:** Fair. Send it.

**JESU:** Two ground rules from my side before I hang up. This first version is a demo - we build it with fake menu data and fake orders. No real customer phone numbers go in until the real launch. We test everything with dummy orders - "Test Thali, quantity 50, address: Nowhere".

**PRANJAL:** Ha. Okay, dummy orders only until I say go.

**JESU:** And no real money moves in the demo. Ever. When we test payments later, that's a separate step with a separate conversation.

**PRANJAL:** Agreed.

**JESU:** Last thing - if this works, what changes for you? What does success look like?

**PRANJAL:** Simple. In the morning I open one screen and see today's orders. No register, no Excel, no duplicate thalis. And I stop answering "where is my order" twenty times a day - they can check themselves.

**JESU:** That's a good spec. One-page note tomorrow, then you decide. Thanks for the five minutes, Pranjal.

**PRANJAL:** Thank you. And Jesu - the biryani is even better when it's fresh. Come to the counter sometime.

**JESU:** (laughs) Deal. Talk tomorrow.

---

## What this call gives the workshop (for the facilitator)

- **Cold-call structure to point out:** introduction (who he is, how he got the number), reason for calling, permission for five minutes, discovery questions, the builder stating scope boundaries, ground rules, a success definition, and one clear next step.
- **Items (menu):** veg thali ₹120, chicken thali ₹180, momos ₹80, chicken biryani ₹200, chowmein ₹90, weekend combos; ~25-30 items; owner-editable with an "available today" toggle (biryani sells out on Sundays).
- **Requirements:** browse menu -> cart -> place order -> customer-visible status (preparing / out for delivery / delivered); kitchen side sees orders immediately and moves them along; one system, no register/Excel copying.
- **Dos:** simple and mobile-first, owner can edit the menu himself, shareable link (WhatsApp status, menu card), demo built with fictional data and dummy orders only.
- **Don'ts:** no payment gateway (cash on delivery only), no live delivery/GPS tracking, no Zomato-style marketplace (no listings, ratings, commissions), no app to install (link/website only), no real customer data or real money in the demo, no scope creep beyond one kitchen.
- **Pain points to echo on slides:** duplicate order entry (register + WhatsApp), end-of-day manual copying, "where is my order?" phone calls.
- **Success definition (the acceptance bar):** one screen with today's orders; no duplicates; customers self-check status.
