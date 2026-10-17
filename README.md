# Torq Legal Labs plugin for Claude

Torq is the intelligence layer for criminal-defense law firms. This plugin gives Claude Torq's guides for firm work, such as designing a client's Gameplan, answering questions from your firm's data and following up on cases. It pairs them with the Torq connector, which gives Claude Torq's tools. The plugin holds guides only: no code, and no firm or client data.

## Who can use it

Members of a Torq firm that has the Torq connector turned on, who hold the "Connect a personal AI assistant to the Brain" permission. A firm admin grants that permission from the member grid in Torq. Each guide works only with the Torq tools your own permissions include.

## Set up

1. Add the plugin. In Claude Code, run:

   ```
   claude plugin marketplace add Torq-Legal-Labs/torq-claude-plugin
   claude plugin install torq-legal-labs@torq-legal-labs
   ```

   On claude.ai and in Cowork, add it under Customize > Plugins. On Team and Enterprise plans, an Owner can add it for the whole organization.

2. Connect the Torq connector and sign in with your Torq account: from the plugin's Connectors tab on claude.ai and in Cowork, or with `/mcp` in Claude Code.

The full setup steps are at https://torqlegallabs.com/claude.

## Use it

Ask Claude in your own words, for example "Design the Gameplan for Maria Lopez" or "How many DUI leads did we sign last month?". Claude loads the matching guide and uses the Torq tools it names. The guides:

- **Build The Firm Brain** (`build-firm-brain`): Build or deepen your firm's Firm Brain by answering Torq's guided interview, one section at a time.
- **Case Operations** (`case-operations`): Ask about a case: its status, upcoming dates and appointments, open tasks, where it sits in a pipeline, or the files attached to it.
- **Case Strategy** (`case-strategy`): Get defense strategy, tactics and investigative questions for a matter, drawn only from your firm's vetted reference-library manuals and cited to them.
- **Finance And Vendor Spend** (`finance-and-vendor-spend`): Ask about your firm's finances: the current snapshot, trends over time, vendor spend and the largest vendor, Brain usage cost, or signed-case revenue by case type.
- **Firm Data Querying** (`firm-data-querying`): Ask questions of your firm's Torq data that the other guides do not cover, such as counts, totals, trends or rankings across leads, cases and opportunities.
- **Design A Gameplan** (`gameplan-design`): Design a client's Gameplan: build, edit, reorder, translate and preview the page, then review and send it from Torq.
- **Intake Coaching** (`intake-coaching`): Ask what good intake looks like, where your intake team is weakest and which practice scenarios fit, and propose scenario assignments for approval.
- **KPI Scorecard Advisor** (`kpi-scorecard-advisor`): Build, prune or fix a team's KPI scorecard: choose the few numbers that matter, set targets from your past data and send the scorecard for approval.
- **Ask The Library** (`library-qa`): Ask a legal or procedural question and get an answer only from your firm's vetted reference-library manuals, with a citation for every claim, or a plain statement that they do not cover it.
- **Marketing Local Services** (`marketing-local-services`): Ask about your firm's Google Local Services Ads: the LSA scorecard, leads that may deserve a rating such as spam, the LSA action queue, or proposing a rating for approval.
- **Memory And Provenance** (`memory-and-provenance`): Ask what earlier conversations in Torq said about something, and where a remembered fact came from.
- **Officer Intelligence** (`officer-intelligence`): Look up an arresting officer by name, badge or department, with the officer's profile, history and linked documents.
- **Owned Media Grounding** (`owned-media-grounding`): Ask what your firm has said publicly about a topic, or get copy grounded in your firm's own published articles and videos, with a link to each source.
- **Reporting And Run History** (`reporting-and-run-history`): Find a saved report and its recipe, check whether a Torq engine is running or failing and how its recent runs went, or look up a Brain workflow run.
- **File A Training Request** (`training-request`): File a training request, flag a process issue or propose an improvement through a guided interview, which points out existing training that may already cover it.

## What it sends

Each tool call goes to Torq's server at mcp.tll.sh under your own Torq sign-in, and Torq applies your permissions to it. What Torq's tools return becomes part of your Claude conversation. The plugin itself stores nothing and sends nothing on its own.

## Privacy and support

- Privacy policy: https://torqlegallabs.com/privacy
- Support: support@torqlegallabs.com

## License

MIT. See [LICENSE](LICENSE).
