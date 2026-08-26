# API Documentation Syllabus

**For:** Salman
**Built:** 26 August 2026
**Project:** Documenting the Airtable Web API — records endpoints
**Three ship dates:** 14 September 2026 · 19 October 2026 · 9 November 2026
**Machine:** MacBook · **Editor:** VS Code · **Accountability:** your wife

---

## How to use this file

Put it in your repo. Open it at the start of each session. Do the next entry. Cross it off.

Each entry has the same six parts:

- **Sessions** — how many evenings it takes
- **Read** — the specific pages, not the chapter
- **Reading for** — the question you're reading to answer
- **Do** — the activity
- **Done when** — the test, so you know whether to move on
- **Bring me** — what to paste into Claude for review

Entries are units of work, not calendar days. Some take one evening, some take three. If an entry runs long, that's information — tell me and I'll re-cut it.

---

## Your constraints (what this plan is built around)

| | |
|---|---|
| Time | 30–40 minutes, weekday evenings only |
| Weekends | Not assumed. If you use them, you're ahead. |
| Code | You don't read any yet. This plan builds that, slowly, reading only. |
| Command line | No experience. **Nothing in cycles 1 and 2 requires a terminal.** |
| Tools | Everything is browser-based or a desktop app with buttons. |
| Book | You own *Docs for Developers*. |
| Machine | MacBook. Terminal, curl and Git are already installed — useful later. |

**The arithmetic, so there are no surprises.** Roughly three hours a week. The original four-week plan assumed ten. So the same work now runs across eleven weeks in three cycles, with your holiday in the middle. Nothing has been cut except the pace.

---

## The rules

1. **Never open a chapter without an entry telling you to.** Sections, not chapters. This is the single change that makes the difference — linear reading has failed three times.
2. **No tracker beyond this file.** No dashboard, no progress percentage, no study app. Maintaining the tracker is not the work.
3. **If an entry isn't done, do it tomorrow. Never extend a ship date.** Ship rough. A published imperfect thing beats an unpublished perfect one.
4. **Everything lands in one GitHub repo,** from day one, including this file.
5. **Tell one named person each ship date.** That person is **your wife**. Tell her the three dates — 14 September, 19 October, 9 November — before you start.
6. **On holiday, 15–27 September: nothing.** No reading, no "light revision," no guilt. That's designed in.

---

## The calendar

### Cycle 1 — Reference documentation
**Thu 27 August – Fri 11 September · 11 sessions · Ship Monday 14 September**

Mon 31 August is the bank holiday — treated as off, and held as your reserve session. Cycle 1 has no slack in it, so if you lose an evening, that's the one to use.

### Holiday
**Tue 15 – Sun 27 September.** Nothing.

### Cycle 2 — The specification
**Mon 28 September – Fri 16 October · 15 sessions · Ship Monday 19 October**

### Cycle 3 — Tutorials, testing, quality
**Tue 20 October – Fri 6 November · 14 sessions · Ship Monday 9 November**

**Why three ship dates, not one.** If the holiday resets you and cycles 2 and 3 never happen, you still have a published API reference on a public URL. The downside is capped before you get on the plane. This is the most important structural decision in the plan.

---

## The project

**API:** Airtable Web API
**Scope — locked, do not expand:** five endpoints against one table in one base you create yourself.

1. List records
2. Get record
3. Create records
4. Update records
5. Delete record

**Why this API:** bearer-token auth with scopes (so you get a real authentication topic to write, not "paste your key in the URL"), full CRUD, offset pagination, rate limits, meaningful error codes — and no official OpenAPI specification published, so writing one in cycle 2 is genuine work rather than transcription.

---

# CYCLE 1 — Reference documentation

**Ship 14 September:** five reference topics, published, on a public URL.

---

### Entry 1.1 — Set up the workspace
**Sessions:** 1 · **Serves:** everything

**Read**
- Johnson, Ch10, *More about Markdown*, pp. 554–560

**Reading for**
- Why plain text rather than Word — the argument, not just the mechanics
- The six things you'll actually use: headings, bold, lists, links, tables, code blocks

**Do**
- Create a public GitHub repo called `airtable-api-docs`
- Install GitHub Desktop (not the command line — the desktop app has buttons) and clone the repo to your machine
- Install VS Code and Postman
- Open the repo folder in VS Code and write the README in Markdown

**Tooling split:** VS Code to write, GitHub Desktop to commit and push. `Cmd+Shift+V` in VS Code gives you a Markdown preview (`Cmd+K` then `V` opens it side by side) — keep it open while you write.

**Done when**
Your README contains two heading levels, a bulleted list, a link, and a code block, and renders correctly on the repo page.

**Bring me**
The repo URL.

---

### Entry 1.2 — What a REST API actually is
**Sessions:** 1 · **Serves:** everything

**Read**
- Johnson, Ch1, *What is a REST API?*, pp. 48–54
- Johnson, Ch1, *Activity 1a: Identify your goals*, p. 55 — actually do this one, in writing
- MDN, *An overview of HTTP*

**Reading for**
- Eight terms you can define without looking: resource, endpoint, method, request, response, status code, header, body
- Why REST is a style and not a standard, and why that means every API is a bit different

**Do**
Create `glossary.md` in the repo. Define all eight in your own words. No copying.

**Done when**
Someone non-technical could read your definitions and follow.

**Bring me**
The eight definitions. I'll correct them — expect at least two to be subtly wrong, which is normal and is the point.

---

### Entry 1.3 — Airtable base and access token
**Sessions:** 1 · **Serves:** all deliverables

**Read**
- Airtable, *Personal access tokens* guide
- Airtable, *Authentication* reference

**Reading for**
- The difference between a scope and base access, and why both must be right
- Why API keys were retired in February 2024

**Do**
- Create a base called `Doc Test`, with one table called `Assets`
- Five fields: a text field, a number, a single-select, a date, and a long-text
- Add six rows of realistic-looking data
- Create a personal access token with scopes `data.records:read`, `data.records:write`, `schema.bases:read`, granted to that base only
- Note the base ID and table name somewhere

**Done when**
Token, base ID and table name are saved somewhere you can find them.

⚠️ The token is displayed **once**. Save it immediately. If you lose it, revoke and recreate. Do not commit it to the repo.

---

### Entry 1.4 — First calls
**Sessions:** 2 · **Serves:** Deliverable 1

**Read**
- Johnson, Ch2, *Get authorization keys*, pp. 73–74
- Johnson, Ch2, *Submit requests through Postman*, pp. 75–81

**Reading for**
- What goes in a header versus a query parameter versus a body
- Why the authorization header is separate from the request itself

**Do**
In Postman, build and save all five requests. Set the bearer token at collection level so you set it once.

**Done when**
All five saved requests return a 2xx, and you have created, changed and deleted a record you can see appear and disappear in the Airtable UI.

**Bring me**
Your POST request and its response, pasted.

**Note on curl.** Johnson teaches curl at pp. 82–97 and it needs a terminal. Skip it for now — Postman shows you the curl equivalent of any request via the `</>` code button, so look at it each time and the syntax becomes familiar by exposure. Worth knowing: curl is already installed on your Mac, so when you do want to run these (tier two, or sooner if curiosity strikes), it's just Terminal and paste. Nothing to install.

---

### Entry 1.5 — Reading a response *(code-reading strand, part 1)*
**Sessions:** 1 · **Serves:** Deliverables 2 and 4

**Read**
- Johnson, Ch2, *Analyze the JSON response*, pp. 98–101
- Johnson, Ch2, *Inspect the JSON from the response payload*, pp. 102–106

**Reading for**
- Object versus array — the only structural distinction that matters
- How to refer in prose to a field nested three levels down

**Do**
Take your list-records response. Write out every field, its type, and what it holds. Include the ones Airtable adds that you didn't create.

**Done when**
You can point at any line of that response and say what it is.

**This is your first code-reading session.** JSON is not a programming language. It's a data format with two shapes and a handful of value types, and it's genuinely learnable in one sitting. Everything else in the strand builds on this.

**Bring me**
Your field list. I'll tell you what you've mislabelled.

---

### Entry 1.6 — Break it on purpose
**Sessions:** 1 · **Serves:** Deliverable 2

**Read**
- Johnson, Ch7, *API status and error codes*, pp. 397–402

**Reading for**
- Why 4xx and 5xx mean fundamentally different things to the reader
- Why the error table is one of the most-visited pages in any API reference

**Do**
Produce five real errors and capture each response verbatim:

1. Wrong or malformed token
2. Valid token missing the required scope
3. Non-existent base or table ID
4. A field name that doesn't exist in your table
5. Deleting a record ID that isn't there

**Done when**
`errors.md` contains five real responses, each with the cause and what the reader should do about it.

**Bring me**
This file. It is the single most valuable thing you produce in cycle 1, because almost nobody writes it and support tickets are almost entirely about it.

---

### Entry 1.7 — The resource description
**Sessions:** 1 · **Serves:** Deliverable 2

**Read**
- Johnson, Ch3, *API reference tutorial overview*, pp. 122–123
- Johnson, Ch3, *Step 1: Resource description*, pp. 124–127
- *Docs for Developers* — the chapter on drafting documentation

**Reading for**
- Why the description comes before the mechanics
- The difference between describing what a resource *is* and what the endpoint *does*

**Do**
Write the resource description for Records.

**Done when**
Five sentences maximum, and a reader who has never used Airtable understands what a record is.

**Bring me**
The paragraph.

---

### Entry 1.8 — Endpoints and methods
**Sessions:** 1 · **Serves:** Deliverable 2

**Read**
- Johnson, Ch3, *Step 2: Endpoints and methods*, pp. 129–133

**Reading for**
- Path parameters versus the base path
- Why the same path with a different method is a different endpoint

**Do**
Write the endpoint and method block for all five, in a consistent format.

**Done when**
Five entries, each with method, full path, and a one-line statement of purpose.

---

### Entry 1.9 — Parameters
**Sessions:** 2 · **Serves:** Deliverable 2 · *This is the hard one*

**Read**
- Johnson, Ch3, *Step 3: Parameters*, pp. 134–142
- Google Developer Documentation Style Guide → *API reference code comments*
- Airtable's own `listRecords` parameter documentation — as a specimen to criticise, not to copy

**Reading for**
- Why required/optional is non-negotiable
- How to document a parameter whose valid values depend on another parameter
- What Airtable does badly here: `fields` and `filterByFormula` are under-explained. Work out why that matters to a reader.

**Do**
Parameter tables for `maxRecords`, `pageSize`, `offset`, `view`, `fields`, `filterByFormula` and `sort` on list records, plus `typecast` and `fields` on the write endpoints.

**Done when**
Every parameter states type, required status, default, constraints, and a description that does not merely restate the parameter's name.

**Bring me**
Your parameter tables. I will be hardest on this entry, because parameter documentation is where the gap between amateur and professional API docs is most visible.

---

### Entry 1.10 — Request and response examples
**Sessions:** 1 · **Serves:** Deliverable 2

**Read**
- Johnson, Ch3, *Step 4: Request example*, pp. 143–153
- Johnson, Ch3, *Step 5: Response example and schema*, pp. 154–166

**Reading for**
- The difference between a response example and a response schema, and why you need both
- How much of a long response to show

**Do**
For each of the five endpoints, include a real request and a real response, trimmed to what illustrates the point.

**Done when**
There is not one placeholder value anywhere in your docs. Every example is something you actually got back.

---

### Entry 1.11 — Assemble and self-review
**Sessions:** 1 · **Serves:** Deliverable 2

**Read**
- Johnson, Ch3, *Putting it all together*, pp. 167–171
- Johnson, Ch3, *Activity: What's wrong with this API reference topic*, pp. 172–175

**Do**
Run that activity against your own five topics rather than his sample. List every fault you find.

**Done when**
You have a written list of your own faults, and have fixed the ones you can in the time left.

**Bring me**
The fault list, and I'll add the ones you missed.

---

### 🚢 SHIP — Monday 14 September
**Sessions:** 1

**Do**
- Repo → Settings → Pages → deploy from `main`
- Confirm the public URL loads
- Send it to your named person

**Done when**
A stranger can read your Airtable records reference documentation at a public URL.

---

# CYCLE 2 — The specification

**Ship 19 October:** a validated OpenAPI specification, rendered as interactive documentation, plus your first conceptual topic.

Everything in this cycle runs in Swagger Editor in the browser. No installs, no terminal.

---

### Entry 2.1 — Re-entry
**Sessions:** 1

**Do**
Read your own cycle 1 documentation cold, after two weeks away. Note everything that confuses you.

**Done when**
You have a list. Two weeks of distance is the cheapest usability test you will ever run — this is why the holiday is useful rather than an interruption.

---

### Entry 2.2 — What a specification is and why anyone bothers
**Sessions:** 1

**Read**
- Johnson, Ch4, *Overview of REST API specification formats*, p. 179
- Johnson, Ch4, *Introduction to the OpenAPI specification*, pp. 180–192

**Reading for**
- Why a machine-readable description beats a hand-written table
- The relationship between the spec, the rendered docs, and the actual API

**Done when**
You can explain to a non-technical colleague what an OpenAPI document is for in two sentences.

---

### Entry 2.3 — YAML *(code-reading strand, part 2)*
**Sessions:** 1

**Read**
- Johnson, Ch5, *Working in YAML*, pp. 267–272

**Reading for**
- Indentation as structure
- Lists versus key-value pairs — the same two shapes you met in JSON

**Do**
Rewrite one of your JSON responses from entry 1.5 as YAML by hand.

**Done when**
It's the same data and you understand why the shapes match. YAML and JSON are the same thing wearing different clothes.

---

### Entry 2.4 — The opening objects
**Sessions:** 1

**Read**
- Johnson, Ch5, *Step 1: The openapi object*, pp. 273–275
- Johnson, Ch5, *Step 2: The info object*, pp. 276–278
- Johnson, Ch5, *Step 3: The servers object*, pp. 279–281

**Do**
Start a new spec in Swagger Editor. Fill in these three objects for the Airtable API.

**Done when**
The editor shows no errors and the right-hand preview shows your API title and version.

---

### Entry 2.5 — The paths object
**Sessions:** 3

**Read**
- Johnson, Ch5, *Step 4: The paths object*, pp. 282–292

**Reading for**
- How a path maps to the endpoint block you already wrote by hand
- Where parameters live, and why some are shared

**Do**
Describe all five endpoints. Work from your own cycle 1 reference topics, not from Airtable's docs — you're converting your own prose into structure.

**Done when**
Five paths, no validation errors.

**Bring me**
The paths section. I'll tell you what a linter would flag before you ever run one.

---

### Entry 2.6 — The components object
**Sessions:** 3

**Read**
- Johnson, Ch5, *Step 5: The components object*, pp. 293–318

**Reading for**
- Why reuse matters — and what breaks when you don't
- The relationship between a schema and the response example you already wrote

**Do**
Define a `Record` schema, a `Records` list schema, an `Error` schema, and reusable parameters for the ones that repeat.

**Done when**
Your paths reference components rather than repeating themselves.

---

### Entry 2.7 — Security
**Sessions:** 1

**Read**
- Johnson, Ch5, *Step 6: The security object*, pp. 319–325

**Do**
Describe Airtable's bearer token scheme.

**Done when**
The rendered output shows an authorize button.

---

### Entry 2.8 — Tags, external docs, and validation
**Sessions:** 1

**Read**
- Johnson, Ch5, *Step 7: The tags object*, pp. 326–328
- Johnson, Ch5, *Step 8: The externalDocs object*, pp. 329–331
- Johnson, Ch5, *Activity: Create an OpenAPI specification document*, p. 332

**Done when**
Zero validation errors in Swagger Editor. Commit the spec to the repo.

---

### Entry 2.9 — Render it
**Sessions:** 1

**Read**
- Johnson, Ch4, *Swagger UI tutorial*, pp. 215–226

**Do**
Get Swagger UI rendering your spec from your GitHub Pages site.

**Done when**
Interactive documentation for your five endpoints exists at a public URL.

---

### Entry 2.10 — Conceptual topic: authentication
**Sessions:** 2

**Read**
- Johnson, Ch7, *API authentication and authorization*, pp. 388–396
- Aaron Parecki, *OAuth 2.0 Simplified* — the introductory chapters only

**Reading for**
- Why authentication is always the first thing a reader needs and the first place they get stuck
- The difference between a token that identifies you and a scope that limits you

**Do**
Write the authentication topic: what a personal access token is, how to create one, which scopes each of your five endpoints needs, and what the failure looks like when a scope is missing — you captured that in entry 1.6.

**Done when**
A reader can go from no token to a working call using only your page.

**Bring me**
The finished topic. This one transfers directly to IAM Cloud work, so it's worth doing properly.

---

### 🚢 SHIP — Monday 19 October

Spec validated, rendered, published, authentication topic live. Tell your named person.

---

# CYCLE 3 — Tutorials, testing, quality

**Ship 9 November:** a getting-started tutorial, a code tutorial, and documentation you've actually tested on a human.

---

### Entry 3.1 — Conceptual topics: pagination and rate limits
**Sessions:** 2

**Read**
- Johnson, Ch7, *API rate limiting and thresholds*, pp. 403–406
- Airtable's pagination and rate limit documentation

**Reading for**
- Why offset-based pagination requires the reader to write a loop, and why that deserves explaining rather than assuming
- What a reader does when they hit a limit

**Do**
Write both topics.

**Done when**
Your pagination topic explains not just what `offset` is, but the pattern for working through every page.

---

### Entry 3.2 — Diátaxis
**Sessions:** 1

**Read**
- diataxis.fr — the whole site. It's short.

**Reading for**
- The four documentation types and why mixing them is the most common structural failure
- How it maps onto the Concept/Task/Reference model you already use

**Do**
Classify every page you've written so far. Note where you've mixed types.

**Done when**
You can articulate the difference between a tutorial and a how-to guide, and you've spotted at least one place you conflated them.

---

### Entry 3.3 — Getting-started tutorial
**Sessions:** 3

**Read**
- Johnson, Ch7, *API getting started tutorials*, pp. 375–387
- Johnson, Ch7, *Activity: Complete the SendGrid Getting Started tutorial*, p. 424 — do it, and note where you got stuck
- *Docs for Developers* — the chapter on tutorials

**Reading for**
- Why a getting-started tutorial has exactly one path and no options
- The ten-minute rule

**Do**
Write it: from nothing to a first successful call.

**Done when**
Someone with an Airtable account and no prior knowledge can succeed in under ten minutes.

---

### Entry 3.4 — Reading code *(code-reading strand, part 3)*
**Sessions:** 2

**Read**
- Johnson, Ch8, *Five strategies for documenting code*, pp. 447–459
- Johnson, Ch8, *Code samples*, pp. 460–471

**Reading for**
- Why explanations should focus on the why rather than the what
- Where the explanation goes relative to the code block

**Do**
Ask me for an annotated Python snippet that pages through all your Airtable records. Explain it back to me line by line. I'll correct you.

**Done when**
You can say what every line does. Not write it — read it. That is the actual job requirement, and Johnson makes this argument himself in Ch12.

---

### Entry 3.5 — The code tutorial
**Sessions:** 2

**Do**
Write the documentation around that snippet: what it does, what to change, what to expect, what goes wrong.

**Done when**
A developer could adapt it to their own base without asking you anything.

---

### Entry 3.6 — Testing
**Sessions:** 2

**Read**
- Johnson, Ch6, *Overview of testing your docs*, pp. 335–336
- Johnson, Ch6, *Test all instructions yourself*, pp. 341–346
- Johnson, Ch6, *Test your assumptions against users*, pp. 347–351

**Do**
Follow your own getting-started tutorial literally, on a fresh base, doing only what it says. Then watch one real person try it. Say nothing while they struggle.

**Done when**
You have a list of failures and have fixed them. Watching someone fail silently is the most uncomfortable and most valuable hour in this syllabus.

---

### Entry 3.7 — Style pass
**Sessions:** 1

**Read**
- Google Developer Documentation Style Guide — *Voice and tone*, *Word list*
- Microsoft Writing Style Guide — the top-level principles, for contrast

**Do**
Edit every page for second person, present tense, active voice, and consistent terminology.

**Done when**
Your terminology is consistent — you don't call it a record on one page and an entry on another.

---

### Entry 3.8 — Review and reflect
**Sessions:** 1

**Read**
- Johnson, Ch9, *4. Reviewing*, pp. 516–523

**Do**
Write a short case study: what you built, what state your understanding was in at the start, what you'd do differently. This is the artifact you show at IAM Cloud when you propose doing it internally.

---

### 🚢 SHIP — Monday 9 November

---

# After 9 November — tier two

Not scheduled. Pick up when the above is done and shipped.

- **Spec governance:** Spectral rulesets and Redocly CLI linting *(requires command line — worth learning at this point, and by then you'll have a reason to)*
- **Docs CI/CD:** GitHub Actions to lint and deploy on every commit
- **API design literacy:** Lauret, *The Design of Web APIs*, then Geewax, *API Design Patterns*
- **Design standards:** Zalando's RESTful API Guidelines and Google's AIPs, read as specimens
- **Error standards:** RFC 9457, Problem Details for HTTP APIs
- **Modern tooling:** Redocly, Scalar, Mintlify, Bump.sh, Docusaurus
- **AI-readable docs:** llms.txt, and structuring documentation for retrieval — direct overlap with your CDM work
- **The internal API at IAM Cloud** — the real target this whole thing has been preparing for
- **Community:** Write the Docs Slack and conference talks

---

# Sources

**Owned**
- Tom Johnson, *Documenting REST APIs* — page references throughout are to your PDFs
- *Docs for Developers* — Bhatti, Corleissen, Lander, Nunez, Waterhouse

**Free, online**
- Google Developer Documentation Style Guide
- Microsoft Writing Style Guide
- Google Technical Writing One and Two
- Diátaxis — diataxis.fr
- MDN HTTP documentation
- Aaron Parecki, *OAuth 2.0 Simplified*
- The OpenAPI Specification itself
- Airtable Web API documentation
- Write the Docs guide

**Tier two, paid**
- Lauret, *The Design of Web APIs*
- Geewax, *API Design Patterns*
- Gentle, *Docs Like Code*

**A note on page numbers.** Johnson's references are exact — I have your PDFs. Book references are by chapter, because I'm not going to invent page numbers I can't verify. Web sources are named by page title; one or two may have moved since I last saw them.

---

# The review loop

This is the part that replaces the subject matter expert you don't have on a public API.

Each entry with a **Bring me** line — paste it into Claude and ask for review. Specifically:

- Reference topics → checked against Johnson's five elements and the Google style guide
- Parameter tables → checked for missing constraints and descriptions that restate the name
- Spec → told what a linter would flag, before you run one
- Response schemas → checked against a real response body you paste
- Explanations → I'll ask you to explain a concept back and find the hole

Explaining something back and being corrected is a better test of understanding than any quiz. Use it every week.

---

## Open assumptions

Flagged rather than guessed at silently:

1. **Weekday evenings only, no weekends.** If weekends are available, cycle 2 could absorb some of cycle 3.
2. **Language for the code tutorial:** Python assumed in entry 3.4, because it reads closest to English. Say if you'd rather PowerShell — it transfers harder to IAM Cloud work but is less pleasant to read cold.

**Resolved:** MacBook. Named person is your wife. Editor is VS Code, with GitHub Desktop for version control. Start date Thursday 27 August.
