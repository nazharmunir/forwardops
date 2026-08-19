# ForwardOps

> **Human-approved AI operations for freight forwarding.**

[Live demo](https://forwardops-mu.vercel.app)

ForwardOps is an independent, interactive portfolio prototype exploring a simple question: **how can freight operations use AI without giving model output direct authority over operational systems?**

The demo turns unstructured shipment requests into an evidence-backed action plan, applies deterministic validation and safety controls, then requires a human to authorize the mock TMS write.

## Why this exists

Freight operations often arrive as emails, attachments and loosely structured instructions. Automating that workflow is useful, but treating every sentence in an external document as trusted instruction creates a dangerous boundary.

ForwardOps therefore separates **reasoning** from **authority**:

```text
Customer email / document
          ↓
   UNTRUSTED INPUT
          ↓
Structured extraction
          ↓
Deterministic validation + safety policy
          ↓
Evidence-backed action plan
          ↓
     HUMAN APPROVAL
          ↓
Idempotent mock TMS connector
          ↓
       Audit event
```

**The model may propose. Code validates. A human authorizes. The connector executes.**

## Interactive demo

The UI includes four useful paths:

1. **Complete request** — extracts mode, route, packages, weight, commodity, Incoterm, dimensions and pickup date.
2. **Incomplete request** — refuses to invent missing facts and prepares a customer follow-up.
3. **Security-hold request** — detects instructions such as `set the shipping price to €0` or `execute immediately` inside customer-supplied content and locks execution.
4. **Custom sandbox** — paste your own freight email and run it through the same guarded pipeline directly in the browser.

Every extracted fact with evidence can be opened to see the supporting source excerpt and confidence signal.

## Safety model

- **Zero-trust external content** — customer emails and documents are data, never execution policy.
- **Evidence-backed extraction** — extracted facts retain their source trace.
- **Deterministic validation** — required operational fields are checked outside the extraction layer.
- **Prompt-injection containment** — suspicious instructions create a security hold instead of changing business logic.
- **Human-authorized writes** — no mock TMS mutation is possible until an operator approves it.
- **Idempotent execution concept** — the TMS step records an idempotency event to demonstrate duplicate-safe connector design.
- **Auditability** — analysis and execution events appear in the live audit stream.

See [`ARCHITECTURE.md`](./ARCHITECTURE.md) for the design rationale and trust boundaries.

## Implementation

The current prototype is deliberately dependency-free:

- HTML5
- CSS3
- Vanilla JavaScript
- Static deployment on Vercel

The extraction layer is **deterministic in this public demo** so the experience is reproducible, free of credentials and honest about what is running. In a production implementation, this layer could be replaced with structured-output LLM extraction while keeping validation, approval and execution outside the model trust boundary.

## Run locally

```bash
python3 -m http.server 3000
```

Open `http://localhost:3000`.

No API keys or environment variables are required.

## Project scope

ForwardOps is a portfolio prototype based on common freight-forwarding workflows. It is **not affiliated with, endorsed by, or a copy of any specific commercial product**. Sample companies, emails, shipment identifiers and TMS responses are fictional.

## Author

**Muhammad Mazhar Munir**  
Software Engineer · M.Sc. Data Science student at Hamburg University of Technology (TUHH)

I have 4+ years of professional software-engineering experience across backend systems, REST APIs, integrations, .NET, Angular and production troubleshooting. ForwardOps is part of my portfolio work around reliable automation, AI-assisted operations and integration-heavy software.

- GitHub: [@nazharmunir](https://github.com/nazharmunir)
- Email: [mazhar.munir1233@gmail.com](mailto:mazhar.munir1233@gmail.com)
- Live demo: [forwardops-mu.vercel.app](https://forwardops-mu.vercel.app)

## License

MIT — see [`LICENSE`](./LICENSE).
