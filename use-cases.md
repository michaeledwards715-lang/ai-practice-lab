# AI Use Cases

A catalog of AI use cases from partnerships, small business, and property management, each sorted by the question *who decides the next step?*

## At a glance

| # | Use case | Type | Who decides the next step | Biggest risk |
|---|---|---|---|---|
| 1 | Partner meeting scheduler | Agent | The AI, based on partner replies | Emails partners as me |
| 2 | Partner deal registration | Workflow | Fixed steps; a person approves the deal | Wrong account or wrong credit |
| 3 | Small business quote requests | Workflow | Fixed steps; a manager approves the quote | Out-of-date prices |
| 4 | Late-rent reminders | Workflow | Fixed dates; the office manager approves the list | Notice to a tenant who already paid |
| 5 | Lease pet-policy check | Workflow | Fixed steps for every new lease; a person spot-checks | Missed or misread lease clause |

## 1. Partner meeting scheduler (EA agent)

**Problem**
Setting up partner meetings takes endless back-and-forth emails to find a time, confirm it, and send invites.

**Type: Agent**
Partner replies are unpredictable ("Tuesday works, but only after 3 my time"), so the AI has to decide its next step as it goes. A simple booking link would handle the easy cases. The agent earns its cost on the messy ones.

**Pieces**
- **Tools (MCP):** Gmail and Google Calendar
- **Memory / context:** a writing style guide so messages sound like me, my scheduling preferences, and a list of which meetings can be moved
- **Instructions:** if no time works, offer the partner alternative options
- **Guardrails:** only book 9 AM to 5 PM Central; only move meetings on the approved list; never cancel a meeting
- **Human-in-the-loop:** I approve outgoing messages, at least at first

**Biggest risk**
It emails partners as me, so one wrong or awkward message can damage a relationship. Booking the wrong time or time zone is the other risk. Limit both with the guardrails above and approval on outgoing messages.

## 2. Partner deal registration (workflow)

**Problem**
Partners email in new deals, and someone has to find the right Salesforce account, record the partner attribution and next steps, and reply. It's slow, manual, and attribution gets missed.

**Type: Workflow**
The steps are fixed every time: read the email, match the account, update Salesforce, reply to the partner.

**Pieces**
- **Tools (MCP):** email, Salesforce, Slack
- **RAG:** the deal registration policy and partner agreements, so it can check whether a deal qualifies or is excluded
- **Human-in-the-loop:** a Slack message to the partner manager, e.g. "This partner registered a deal. Here are the two matching accounts. Which one, and do you approve?"
- **Guardrails:** it can update only the partner and next-step fields, and can never create or delete accounts

**Biggest risk**
Approving a deal decides credit, commission, and possible conflict with the direct sales team, so the AI only recommends and a person approves. It could also match the wrong account (duplicates are common), so uncertain matches always go to a person.

## 3. Small business quote requests (workflow)

**Problem**
A small business gets many quote requests by email every day, and building each quote by hand is slow.

**Type: Workflow**
Fixed steps: spot the quote request, identify the product and volume, look up pricing, draft the quote, get approval, send.

**Pieces**
- **Tools (MCP):** Gmail and the price list (Google Sheet or Excel)
- **Direct lookup for prices:** exact prices come straight from the sheet, not from the AI's memory, to avoid hallucinated numbers
- **RAG:** product descriptions, to match fuzzy requests to the right product
- **Human-in-the-loop:** a manager approves each quote before it goes to the customer
- **Guardrails:** any discount request over 2% goes to the manager

**Biggest risk**
An out-of-date price list means quotes go out at the wrong price, possibly at a loss. Limit it by assigning an owner to update the price list on a set schedule, and showing the "last updated" date on every quote for approval.

## 4. Late-rent reminders (workflow)

**Problem**
Every month the office checks who hasn't paid, sends a reminder on the 5th, a second notice on the 10th, and then hands unpaid accounts to the property manager. It's repetitive, and easy to miss someone or send to the wrong person.

**Type: Workflow**
The dates and steps are the same every month: check payments, send notice 1, check again, send notice 2, hand off. Nobody needs the AI to decide what to do next.

**Pieces**
- **Tools (MCP):** the rent payment system (read-only) and email
- **Human-in-the-loop:** the office manager reviews the list of tenants flagged as late before any notice goes out
- **Guardrails:** only send pre-approved notice templates; never change balances or add late fees; skip anyone on a payment plan

**Biggest risk**
A tenant who paid, but whose payment wasn't logged yet, gets a late notice. That makes for an angry tenant and possible legal trouble. Limit it by having a person approve the list each month, and by using notice wording a lawyer has signed off on.

## 5. Lease pet-policy check (workflow)

**Problem**
A 400-unit property manager can't quickly answer "which leases allow pets?" Someone has to open and read each lease PDF, and new leases keep arriving.

**Type: Workflow**
It comes up with every new lease, so the steps are fixed: a new lease lands in the folder, the AI finds the pet clause, records the answer and the exact wording in a tracking sheet, and flags anything unclear. (The first pass over the existing 400 leases is a one-time batch run of the same steps.)

**Pieces**
- **Tools (MCP):** Google Drive (read-only, the leases folder) and a Google Sheet to record results
- **RAG:** the AI looks up the pet clause in each lease and quotes the exact wording, so every answer can be checked against its source
- **Human-in-the-loop:** pilot on 100 leases, and the office manager spot-checks 20; roll out to all 400 only if the AI matches on at least 19 of 20. Afterwards, anything marked "unclear" goes to a person.
- **Guardrails:** read-only access to leases; it never edits a lease or contacts a tenant

**Biggest risk**
It misses or misreads a clause (for example, a pet addendum filed separately, or "cats only"), and the office acts on the wrong answer. Limit it by always quoting the exact lease wording, sending unclear cases to a person, and spot-checking a sample each quarter.
