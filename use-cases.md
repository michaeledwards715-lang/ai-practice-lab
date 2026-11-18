# AI Use Cases

Three use cases from partnerships and small business, each sorted by the question *who decides the next step?*

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
