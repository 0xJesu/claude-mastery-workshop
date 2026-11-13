# Fictional Client Call Transcript: Food-Ordering E-Commerce App

**Claude Mastery Workshop, 14 Nov 2026 - Requirements Exercise**

> **This transcript is fictional.** It was written for a classroom exercise. The business, the people and every detail in it are invented, and it does not record a real call. Use it to practice turning a messy client conversation into requirements, a small spec and a working first slice.

*Setting: A developer who builds small software for local businesses takes a discovery call from the owner of a small restaurant in Karol Bagh, Delhi. The call lasts about 15 minutes. Speakers: JESU (the developer) and PRANJAL (owner of "Deka's Kitchen", an invented business).*

---

## Transcript

**JESU:** Hello, Pranjal? Jesu here. You said you wanted to talk about getting orders online?

**PRANJAL:** Yes, yes. Thanks for calling back. So - I run a small kitchen in Karol Bagh. Lunch and dinner. Thalis, momos, biryani, chowmein. The usual stuff people order every day.

**JESU:** Okay. And how do orders come in today?

**PRANJAL:** Phone calls. Mostly phone calls, some WhatsApp messages. My guy writes them in a register, then at the end of the day someone copies everything into an Excel sheet. Yesterday we found the same order entered twice - one from the register, one from the WhatsApp message. The customer got two thalis and paid for one. (laughs) He was happy. I was not.

**JESU:** (laughs) Okay, so duplicates are a real problem. What do you want instead?

**PRANJAL:** Simple thing. A website where the customer sees my menu, picks what they want, and places the order themselves. It goes straight into one system. No register, no copying, no double entry.

**JESU:** Got it. Walk me through the menu a bit - how many items are we talking?

**PRANJAL:** Around 25-30 items. Veg thali 120, chicken thali 180, momos 80 a plate, chicken biryani 200, chowmein 90. A few combos on weekends. Prices change maybe once in two-three months. I should be able to edit the menu myself - mark something "not available today" when it runs out. That happens with biryani almost every Sunday.

**JESU:** So a menu you can edit, with an available/not-available switch. What happens after the customer places an order?

**PRANJAL:** My kitchen should see it immediately - new order, items, quantity, customer name, phone, address. Then we mark it: preparing, then out for delivery, then delivered. The customer should be able to check the status themselves instead of calling me five times. "Where is my order?" - I get this twenty times a day.

**JESU:** Okay: menu, cart, place order, order status, and a simple kitchen side to move the order along. Now let me tell you what I will NOT build in the first version, and you tell me if that's okay.

**PRANJAL:** Go ahead.

**JESU:** One - no online payment. No UPI gateway, no card. Cash on delivery only. Payment gateways need documents, verification, and they take a cut. We can add it later.

**PRANJAL:** Fine. Most of my customers pay cash anyway.

**JESU:** Two - no delivery tracking on a map. No rider locations, no live GPS. Your delivery boy is not getting tracked.

**PRANJAL:** (laughs) He's my nephew, he would quit. Okay, no maps.

**JESU:** Three - and I want to be very clear here - this will not be Zomato. No restaurant listings, no ratings, no discovery, no commissions page. Just YOUR kitchen, YOUR menu, YOUR orders. One shop, online.

**PRANJAL:** That's exactly what I want. I don't want to be on Zomato, they take too much commission. I want my own thing. I can put the link on my WhatsApp status and on the menu card.

**JESU:** Perfect. Now some ground rules from my side. This first version is a demo - we build it with fake menu data and fake orders. No real customer phone numbers go in until the real launch. We test everything with dummy orders - "Test Thali, quantity 50, address: Nowhere".

**PRANJAL:** Ha. Okay, dummy orders only until I say go.

**JESU:** And no real money moves in the demo. Ever. When we test payments later, that's a separate step with a separate conversation.

**PRANJAL:** Agreed.

**JESU:** Last thing - what does "success" look like to you? If this works, what changes?

**PRANJAL:** Simple. In the morning I open one screen and see today's orders. No register, no Excel, no duplicate thalis. And I stop answering "where is my order" twenty times a day - they can check themselves.

**JESU:** That's a good spec. Let me write this up as a one-page requirements doc and send it to you. You read it, correct whatever I got wrong, and once you say yes, that's exactly what we build.

**PRANJAL:** Sounds good. When can you send it?

**JESU:** Tomorrow. Talk then.

---

## What this call gives the workshop (for the facilitator)

- **Items (menu):** veg thali ₹120, chicken thali ₹180, momos ₹80, chicken biryani ₹200, chowmein ₹90, weekend combos; ~25-30 items; owner-editable with an "available today" toggle (biryani sells out on Sundays).
- **Requirements:** browse menu -> cart -> place order -> customer-visible status (preparing / out for delivery / delivered); kitchen side sees orders immediately and moves them along; one system, no register/Excel copying.
- **Dos:** simple and mobile-first, owner can edit the menu himself, shareable link (WhatsApp status, menu card), demo built with fictional data and dummy orders only.
- **Don'ts:** no payment gateway (cash on delivery only), no live delivery/GPS tracking, no Zomato-style marketplace (no listings, ratings, commissions), no real customer data or real money in the demo, no scope creep beyond one kitchen.
- **Pain points to echo on slides:** duplicate order entry (register + WhatsApp), end-of-day manual copying, "where is my order?" phone calls.
- **Success definition (the acceptance bar):** one screen with today's orders; no duplicates; customers self-check status.
