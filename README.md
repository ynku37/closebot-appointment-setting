# closebot appointment setting: How the AI books appointments in your CRM, what each plan costs, and the calendar mistakes that break it

Appointment setting with AI sounds like a one-line pitch: connect a calendar, let the bot chat, watch bookings appear. What actually decides whether it works is narrower than most people expect. It comes down to whether the agent is on a booking action at the right moment, whether your calendar is readable, and whether the contact record has enough data to place the event.

CloseBot is built specifically for that job. It qualifies leads, follows up, and books appointments across your existing HighLevel, HubSpot, or custom CRM. Below is how the appointment-setting side actually works, what each plan costs right now, and the specific setup errors that make an agent say "you're booked" while your calendar stays empty.

## What CloseBot is, in appointment-setting terms

CloseBot is a conversational AI layer that sits on top of a CRM rather than replacing it. You build an agent with objectives, knowledge, and tools, connect a source (HighLevel, HubSpot, LeadConnector, or a custom setup), and the agent takes over text-based conversations already flowing through that CRM.

That architecture matters for appointment setting in two ways.

First, the agent is **agentic, not rule-based**. You describe what a conversation needs to achieve and the agent reasons through it. CloseBot describes the four building blocks as objective-driven conversations, a drag-and-drop builder, a testing portal, and Smart FAQ.

Second, it is **CRM-native**. CloseBot does not connect to Instagram or WhatsApp by itself. If your DMs are connected inside your CRM inbox, the agent can answer them. If your pipeline lives entirely in a DM tool with no CRM underneath, you would be adding one before you get any bookings.

👉 [Start a free CloseBot account and build a booking agent](https://app.closebot.com/a?fpr=li87)

## How CloseBot actually books an appointment

The booking step is a single action inside a job flow. Here is the sequence that matters, based on CloseBot's own documentation.

**1. Connect a source.** The source is your CRM connection and the thing that supplies calendars and contact records. One agent can work across unlimited accounts within a niche.

**2. Add a booking action at the point where you want the appointment offered.** Actions run in order, so the agent handles qualification first and only reaches booking when the flow says so.

**3. Pick a calendar, by name or by ID.** Selecting the calendar name from the dropdown auto-fills the appointment title and short description. Selecting "Other – Use Calendar ID" requires the *permanent* calendar ID from your CRM. This ID is what lets one agent route different leads to different calendars, which is how clinics split bookings by treatment type, or how a sales team sends different lead types to different reps.

**4. Set the short description.** Keep it minimal: appointment type and duration. "Book a 30 minute in-person appointment," not a paragraph.

**5. Handle time zones deliberately.** Conversational booking uses the contact's time zone when it exists on the contact record, and falls back to the source's time zone when it does not. If your contacts book from other time zones, you need an objective *before* the booking action that collects and updates the contact's time zone. Otherwise you will book people at the wrong hour and they will simply not show up.

**6. Turn on rescheduling if you want it.** Conversational rescheduling is disabled by default. It lives in Job Flow Settings → Important Business Info. Once enabled, the agent can move any appointment it finds for a contact, including ones it did not book itself.

One technical detail worth internalizing: **the agent is blind to your availability unless it is on a booking objective.** When the booking action runs, CloseBot requests available times from the connected calendar, factoring in user availability, calendar settings, and meeting duration, then the agent offers slots that match what the contact said. You can hover the calendar icon on that message in the dashboard to see exactly what availability it pulled.

## Where appointment setting breaks (and how to fix it)

CloseBot's troubleshooting documentation is unusually candid about failure modes. These are the ones that cost bookings.

**The agent confirms a booking that never lands on the calendar.** This is almost always the same root cause: the word "appointment" or "booking" appears somewhere else in your settings, usually in Important Business Information or the "Why the conversation is happening" section. Because actions run in sequence, stray booking language makes the agent talk about scheduling before it is actually on the booking step.

**No slots found.** The agent pulls live availability. If your calendar has no open times, it will say so. Check that the calendar exists, is active, and has not been set to draft.

**Calendar ID not working.** If you use the custom calendar ID option for GoHighLevel or LeadConnector, it must be the permanent ID. Temporary or display IDs will fail silently.

**The contact has no phone number or email.** Conversational booking needs at least one. Add an objective that collects contact details before the booking action.

**Wrong availability quoted.** Use the reasoning/logs view on that message to see the timezone and availability the agent actually received. If the location time zone cannot be pulled, CloseBot falls back to Eastern Time, which is a common source of weird slot offers for non-US businesses.

CloseBot also flagged a date-arithmetic problem in its own docs where agents mixed up weekdays on Anthropic models, with the recommended fix being a provider change. In one published case study, a partner hit a recalculating date bug four or five times before CloseBot patched around it with a validation wrapper that checks the proposed date against the stated weekday before sending it to the calendar. Weekday math is a known weak spot across LLMs, and it is worth testing your own agent against it before going live.

## What appointment setting with CloseBot costs

CloseBot's plans page currently shows four plan shapes. Business plans include message costs in the base price, which is the detail most competitors do not offer.

| Plan | Best for | Messages and limits | Price | Billing | Get started |
| --- | --- | --- | --- | --- | --- |
| Free | Testing the agent, or very low lead volume | 100 messages/mo, 1 agent, 1 user seat, 1 MB knowledge storage, unlimited account connections | $0 | Free forever | [Start on the free plan](https://app.closebot.com/a?fpr=li87) |
| Core (Business) | Businesses booking their own leads | 500 messages included in the base price, 15+ templates, human support, extra seats $5/user, storage add-ons | from $64/mo; $53/mo billed as $640/yr on annual | Month to month or annual | [See the Core business plan](https://app.closebot.com/a?fpr=li87) |
| Core (Agency) | Agencies building and rebilling agents for clients | Unlimited messages at $0.012/message, rebillable; white-label client portal; rebill all costs | $397/mo | Month to month or annual | [Compare the Agency plan](https://app.closebot.com/a?fpr=li87) |
| Growth | Regulated or high-volume operations | 50+ templates, HIPAA compliance, quarterly audits, 99.99% priority uptime, priority support | Custom | Contact sales | [Talk to CloseBot about Growth](https://app.closebot.com/a?fpr=li87) |

A few cost mechanics that catch people out:

- **You choose your monthly message ceiling.** The business plan starts at 500 messages, and the plans page scales across tiers up to 100K+ messages a month. Higher ceilings cost more, and the higher you go, the better the bulk pricing.
- **Overage is not free.** On business plans, messages beyond your ceiling are billed at a 2x rate drawn from a wallet. On the free plan, extra messages run $0.08 each. If you exceed 100 messages regularly, the free plan is not the plan you want.
- **Storage is metered.** Business plans include 1 MB and then charge between $0.10 and $3.00 per MB per month depending on how much you need. For reference, CloseBot estimates 1 MB of text is roughly 1,000 pages.
- **Seats cost $5 per additional user.** One is included.
- **CloseBot does not issue refunds.** Instead there is a free-forever plan under 100 messages and a 7-day trial of any paid plan, including Agency. Plans are month to month with no contract.

CloseBot also lists an official discount code on its own coupon page, `CLOSEBOT100OFF`, for $100 off a first payment. Use it at checkout if it is still live; if a code fails, CloseBot's guidance is to contact them rather than hunt coupon aggregator pages.

## Business plan or agency plan?

The split is not about message volume, it is about who pays.

If you are booking your own leads, the business track is the sensible one. Message costs are folded into the subscription, so your bill does not move every time an agent has a busy week. That predictability matters more than the headline price when you are forecasting.

If you are selling AI appointment setting as a service, the agency plan changes the economics. You pay $0.012 per message and set your own markup, clients top up wallets that pay you through your Stripe account, and the white-label portal means your logo is on what they log into. One published agency case study on CloseBot's plans page bills an average of $500 per client per month. At that spread, the platform fee is the smaller number in the equation.

The awkward middle case: a solo operator who wants to resell later but has two clients today. Business plans do not expose rebilling or white labeling, which is why CloseBot points those users to the Agency trial.

## What you get beyond the booking step

Booking is the outcome, but the supporting features decide your booking rate.

**Smart FAQ** watches for questions the agent cannot answer confidently and flags them instead of inventing an answer. When you answer, CloseBot can follow up with every lead who asked. For appointment setting, that is the difference between a hallucinated promise and a booked call.

**Smart follow-up** reads commitments in the conversation. In a case study CloseBot published with agency owner Mike Oddo, a lead who filled a form after midnight and said "not right now" got followed up three days later and booked, with scheduled follow-up sequences turned off.

**Message splitting** breaks replies into short, separately timed texts instead of one block. It sounds cosmetic and is not: nobody reads a five-line paragraph from an unknown number.

**Provider choice** lets you pick between multiple LLM providers, with automatic fallback to your other preferred models if the primary one fails. Response quality varies noticeably between models, and so does cost.

**Testing portal and rollback.** You can test conversations, including bookings, before going live, pause the AI on any conversation for a human takeover, and revert changes.

**Custom tools.** If something you need does not ship with the product, you can register your own tool and let the agent call it. The Oddo case study used this to check drive time before booking, so a crew's appointments cluster geographically.

CloseBot's marketing numbers are worth reading as marketing: over 1 million booked appointments, roughly 150K messages a day, 99.99% uptime, 40+ languages, and 1,000+ agencies on the platform. Vendor figures, not audited ones. Independent signals lean positive though. On G2, a reviewer described it as the best AI agent for text responses among the chat platforms their team tested, and in a Reddit thread comparing it to GoHighLevel's native Conversation AI, a user noted conversational booking and rescheduling work well.

## The honest limits

CloseBot needs a CRM underneath it. If your leads live in Instagram DMs and you run no CRM, you are buying two products to do one job.

No AI setter closes deals, including this one. The agent qualifies, follows up, and puts a qualified call on the calendar. The close happens on the call with a human.

Weekday arithmetic remains the weakest technical link in conversational booking across the category, and it is worth testing hard with real dates, including month boundaries, before you let an agent loose on live leads.

And the pricing model rewards scale rather than punishing it, but only if you actually track message volume. A chatty agent on a business plan with a low ceiling will burn through overage at 2x rates before you notice.

## FAQ

**Does CloseBot need GoHighLevel?**
No. It integrates natively with HighLevel and HubSpot, and supports LeadConnector and custom CRM sources. HighLevel is the most common setup, not a requirement.

**How fast does the agent reply to a new lead?**
CloseBot states typically within 3–5 seconds, triggered off a web chat widget or a webhook from a form submission.

**Can one agent book to different calendars?**
Yes. Booking by calendar ID is the mechanism, and it is how clinics split by treatment and sales teams split by lead type.

**Can it reschedule appointments?**
Yes, but conversational rescheduling is off by default. Enable it in Job Flow Settings → Important Business Info.

**Is there a free trial?**
There is a free-forever plan capped at 100 messages a month, plus a 7-day trial of any paid plan before billing starts. No refunds after that.

**What does HIPAA compliance require?**
HIPAA is available on Growth plans only, and CloseBot's docs note it currently routes HIPAA accounts to Anthropic as the provider.

If you want to see how the booking flow behaves with your own calendar and leads, the free plan is the cheapest way to find out.

👉 [Create your free CloseBot account and test appointment booking](https://app.closebot.com/a?fpr=li87)
