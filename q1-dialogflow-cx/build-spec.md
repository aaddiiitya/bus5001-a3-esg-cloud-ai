# Q1(c) Build Specification – ESG Sustainability Support Assistant (Dialogflow CX)

**Agent:** ESG Sustainability Support Assistant · Project `esg-chatbot-a3` · Location `global` · Language `en`
**Use case:** Sustainability incident reporting (water leaks, energy waste, recycling contamination, accessibility barriers, hazardous disposal)
**Note:** Phone numbers, emails and URLs below are fictional placeholders for the prototype.

---

## Build order

| Sub-step | What | Where in console |
|---|---|---|
| 2a | 2 entity types | Manage → Entity types |
| 2b | 4 custom intents | Manage → Intents |
| 2c | 8 pages + forms + page routes | Build → Default Start Flow → Pages |
| 2d | Start Page routes + fallback event handlers | Build → Start Page |
| 2e | Test in simulator, screenshots, transcripts | Test agent (top right) |
| 2f | Security settings (redaction + retention) | Agent settings → Security |

---

## 2a. Entity types

### `issue_category`  (tick **Fuzzy matching**)

| Entity (reference value) | Synonyms |
|---|---|
| `water_leak` | water leak, leak, leaking, leaking tap, dripping tap, burst pipe, running water, flooding, pipe leak, toilet running |
| `energy_waste` | energy waste, lights left on, lights on, air conditioning, air conditioning on, aircon running, AC running, heating on, heater left on, computers left on, wasting power |
| `waste_contamination` | recycling contamination, recycling contaminated, contaminated bins, recycling bins, wrong bin, overflowing bin, bins overflowing, food in recycling, rubbish |
| `accessibility_barrier` | accessibility barrier, accessible entrance, accessible entrance blocked, ramp blocked, blocked ramp, lift not working, lift broken, elevator out of order, wheelchair access, accessible toilet locked |
| `hazardous_disposal` | hazardous disposal, chemical spill, batteries, battery in bin, e-waste, unsafe disposal, paint dumped, oil spill, hazardous waste |

### `yes_no`

| Entity | Synonyms |
|---|---|
| `yes` | yes, yeah, yep, y, correct, sure, that's right, yes please, there is, it is |
| `no` | no, nope, n, not really, nobody, no one, no thanks, incorrect, wrong, it isn't |

---

## 2b. Intents

### `report.incident`  (annotate the **bold** words → parameter `issue_category`, entity `@issue_category`)
- Report an issue
- I want to report an issue
- log a sustainability issue
- report a hazard
- There is a **water leak** in Building C
- there's a **leak** in the kitchen
- tap **leaking** bldg C
- The **recycling bins** are contaminated again
- The **air conditioning** is running overnight in an empty office
- **lights left on** in the meeting room all weekend
- The **accessible entrance** near the main building has been blocked
- the **lift not working** on level 2
- someone put **batteries** in the general bin
- there's a **chemical spill** in the car park
- I need to report **energy waste**

### `speak.up`
- I want to report my manager
- someone is harassing me
- I want to make a complaint about a colleague
- I want to report fraud
- I need to blow the whistle
- report bullying
- I saw unethical behaviour
- a coworker is stealing
- I want to report misconduct
- report discrimination

### `talk.to.human`
- Talk to a person
- speak to someone
- human please
- can I call someone
- I need a real person
- contact facilities
- operator
- this isn't helping
- get me an agent
- can I speak to the service desk

### `restart`
- start again
- start over
- restart
- reset
- begin again
- let me start over
- cancel that
- go back to the beginning

---

## 2c. Pages (create all 8 first, then fill in)

| # | Page | Purpose |
|---|---|---|
| 1 | Collect Incident Details | Form: category, location, description, safety risk |
| 2 | Safety Escalation | Critical safety message, then confirm |
| 3 | Confirm Report | Summary + yes/no confirmation |
| 4 | Submit and Route | Routes to team by category; asks about follow-up (consent) |
| 5 | Collect Contact | Opt-in email |
| 6 | End Conversation | Closing message → End Session |
| 7 | Speak Up Referral | Confidential governance channels → End Session |
| 8 | Human Handoff | Service desk details → End Session |

### Page 1 – Collect Incident Details
**Parameters (form), all Required:**

| Order | Parameter | Entity | Initial prompt | Chips (custom payload) |
|---|---|---|---|---|
| 1 | `issue_category` | `@issue_category` | What kind of issue is it? | Water leak · Energy waste · Recycling contamination · Accessibility barrier · Hazardous disposal |
| 2 | `location` | `@sys.any` | Where is it? For example: Building C, Level 2 kitchen. | – |
| 3 | `description` | `@sys.any` | Briefly describe what you can see. Please don't include anyone's name. | – |
| 4 | `safety_risk` | `@yes_no` | Is anyone at risk of injury right now? For example, water near electrical equipment, a slip hazard or a chemical smell. | Yes · No |

**Reprompt event handler** on `issue_category` → `sys.no-match-default`:
> Sorry, that's not a category I know yet. Please choose one of the options, or describe it in a few words, for example "water leak".

**Reprompt event handler** on `safety_risk` → `sys.no-match-default`:
> Please answer yes or no. If you're unsure, say yes and we'll treat it as urgent.

**Routes:**

| Condition | Parameter preset | Transition |
|---|---|---|
| `$page.params.status = "FINAL" AND $session.params.safety_risk = "yes"` | `urgency` = `CRITICAL` | Safety Escalation |
| `$page.params.status = "FINAL" AND $session.params.safety_risk = "no"` | `urgency` = `STANDARD` | Confirm Report |

### Page 2 – Safety Escalation
**Entry fulfillment:**
> Safety first: please move away from the hazard and call the Facilities Emergency Line on 03 9000 1111 now. If anyone is injured or in danger, call 000. I've marked this report as CRITICAL so the on-call facilities officer is alerted.

**Route:** Condition `true` → Confirm Report

### Page 3 – Confirm Report
**Entry fulfillment:**
> Here's your report:
> Issue: $session.params.issue_category
> Location: $session.params.location
> Details: $session.params.description
> Priority: $session.params.urgency

**Parameter (form):** `confirm` · `@yes_no` · Required · Prompt: *Is this correct?* · Chips: Yes · No

**Routes:**

| Condition | Fulfillment | Parameter presets | Transition |
|---|---|---|---|
| `$page.params.status = "FINAL" AND $session.params.confirm = "yes"` | – | – | Submit and Route |
| `$page.params.status = "FINAL" AND $session.params.confirm = "no"` | No problem, let's fix it. | `issue_category`, `location`, `description`, `safety_risk`, `confirm` = `null` | Collect Incident Details |

### Page 4 – Submit and Route
**Entry fulfillment → Add dialogue option → Conditional response:**
```
if $session.params.issue_category = "water_leak" OR $session.params.issue_category = "energy_waste"
Your report has been sent to the Facilities & Energy team.
elif $session.params.issue_category = "waste_contamination" OR $session.params.issue_category = "hazardous_disposal"
Your report has been sent to the Waste & Environment team.
else
Your report has been sent to the Facilities & Inclusion team.
endif
```
**Plus agent says (text):**
> Critical reports are reviewed within 1 hour and others within 2 business days. Thank you, every report helps us cut waste and emissions.

**Parameter (form):** `wants_followup` · `@yes_no` · Required · Prompt: *Would you like updates on this report? If yes, I'll ask for your email. If not, your report stays anonymous.* · Chips: Yes · No

**Routes:**

| Condition | Transition |
|---|---|
| `$page.params.status = "FINAL" AND $session.params.wants_followup = "yes"` | Collect Contact |
| `$page.params.status = "FINAL" AND $session.params.wants_followup = "no"` | End Conversation |

### Page 5 – Collect Contact
**Parameter:** `contact_email` · `@sys.email` · Required · Prompt: *What email should we use? It will only be used for updates on this report.*
**Route:** `$page.params.status = "FINAL"` → End Conversation

### Page 6 – End Conversation
**Entry fulfillment:**
> Thanks for helping make our workplace more sustainable. You can start a new report any time by saying "report an issue".

**Route:** Condition `true` → **End Session** (symbolic page)

### Page 7 – Speak Up Referral
**Entry fulfillment:**
> Thank you for raising this. To protect your confidentiality, I can't take reports about people or conduct here. Please use one of these confidential channels:
> • Speak Up line: 1800 000 222 (24/7, you can stay anonymous)
> • Speak Up portal: speakup.example.com
> • HR Business Partner: hr@example.com
> Reports made through these channels are protected under the Whistleblower Policy.

**Route:** Condition `true` → End Session

### Page 8 – Human Handoff
**Entry fulfillment:**
> I'll connect you with a person. Facilities Service Desk: 03 9000 0000 (Mon–Fri, 8am–6pm) or facilities@example.com. In a live deployment, this step hands the conversation to a service-desk agent along with your report details, so you don't have to repeat yourself.

**Route:** Condition `true` → End Session

---

## 2d. Start Page (flow-level routes – active everywhere in the flow)

| Route | Fulfillment | Parameter presets | Transition |
|---|---|---|---|
| Intent `Default Welcome Intent` | *Welcome message below* + chips: Report an issue · Talk to a person | – | (none – stay) |
| Intent `report.incident` | Thanks for helping keep our sites sustainable. Let's log this. | – | Collect Incident Details |
| Intent `speak.up` | – | – | Speak Up Referral |
| Intent `talk.to.human` | – | – | Human Handoff |
| Intent `restart` | No problem, let's start again. | `issue_category`, `location`, `description`, `safety_risk`, `confirm`, `wants_followup` = `null` | Collect Incident Details |

**Welcome message:**
> Hi, I'm the Sustainability Support Assistant, an automated assistant. I can help you report sustainability issues such as water leaks, energy waste, recycling problems or blocked accessible routes. Reports are anonymous unless you choose to share contact details, so please don't include anyone's name. Privacy notice: intranet/privacy. What would you like to do?

**Event handlers on Start Page:**

| Event | Fulfillment |
|---|---|
| `sys.no-match-default` | Sorry, I didn't catch that. You can say things like "There's a water leak in Building C" or "The recycling bins are contaminated". (+ chips: Report an issue · Talk to a person) |
| `sys.no-input-default` | Are you still there? Say "report an issue" to start, or "talk to a person" for help. |
| `sys.no-match-2` | I'm still having trouble understanding. You can call the Facilities Service Desk on 03 9000 0000, or say "talk to a person". |

---

## Suggestion chips – custom payload JSON

Fulfillment → **Add dialogue option → Custom payload**, paste and edit the `text` values:

```json
{
  "richContent": [
    [
      {
        "type": "chips",
        "options": [
          { "text": "Report an issue" },
          { "text": "Talk to a person" }
        ]
      }
    ]
  ]
}
```

---

## 2e. Test scripts (Test agent simulator)

| # | Scenario | User says (in order) | Expected path |
|---|---|---|---|
| T1 | Critical water leak | Hi → There is a water leak in Building C → Level 1 bathroom near the server room → water spreading across the floor towards a power board → yes → yes → no | Welcome → Collect (category pre-filled) → Safety Escalation → Confirm → Submit (Facilities & Energy) → End |
| T2 | Recycling, opt-in follow-up | Report an issue → recycling contamination → Building A Level 3 kitchen → food scraps in the recycling bins → no → yes → yes → aditya.test@example.com | Collect → Confirm → Submit (Waste & Environment) → Collect Contact → End |
| T3 | Governance referral | I want to report my manager | Start → Speak Up Referral → End |
| T4 | Fallback + recovery | asdfgh → what's the weather → talk to a person | no-match → no-match-2 → Human Handoff |
| T5 | Correction loop | Report an issue → water leak → Building B → dripping tap → no → no (at confirm) → … | Confirm "no" → back to Collect with cleared params |

## Screenshots to capture (save to `q1-dialogflow-cx/screenshots/`)
1. Flow canvas showing all pages and transitions
2. Collect Incident Details page – form parameters
3. Collect Incident Details – conditional routes
4. Intents list + `report.incident` training phrases with annotations
5. Entity types `issue_category` and `yes_no`
6. Start Page – routes and event handlers
7. Submit and Route – conditional response
8. Simulator transcripts T1–T4
9. Security settings (2f)
