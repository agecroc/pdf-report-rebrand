--- name pdf-report-rebrand description Ingest full PDF reports, produce a uniquely interpreted and fully rebranded branded report (cover, colors, graphics, layout), generate a PowerPoint summary for employee education, and export slides to Notlm for animated YouTube content. Use when transforming third-party or internal reports into SMAART Company branded assets for customer marketing, internal training, and social video publishing. ---

1. Collect the source PDF, brand guidelines (logo, colors, fonts), target audience (customers or employees), and output destinations (branded PDF, PowerPoint, Notlm/YouTube).
2. Extract and reinterpret all text content into original insights aligned with SMAART Company voice.
3. Rebrand all visual elements: cover page, color palette, charts, icons, and section headers.
4. Produce the final branded PDF report for customer distribution or internal use.
5. Distill key insights into a PowerPoint deck structured for employee education.
6. Export PowerPoint slides to Notlm for animation rendering.
7. Publish animated video to YouTube and distribute branded PDF as lead-gen or employee resource.

TITLE PDF Report Rebrand - Quick Start

Collect:
- Source PDF (full report)
- Brand kit: logo, primary/secondary colors (hex), approved fonts
- Target audience: customers (lead-gen/value) or employees (education)
- Distribution channels: website, email, internal portal, YouTube
- Notlm project credentials and animation style preferences

Reject vague inputs. Require brand hex codes and confirmed output destinations before proceeding.

TITLE PDF Report Rebrand - Design Procedure - 1. Define Scope

Break the pipeline into these deterministic stages:
- Trigger: PDF received (upload or URL)
- Extract: Parse all text, data, and graphic references
- Reinterpret: Rewrite content in SMAART Company voice with unique insights
- Rebrand: Apply brand cover, colors, fonts, charts, icons
- Output PDF: Render final branded report
- Distill: Identify top 10-15 insights for slides
- Build PPT: Generate PowerPoint with branded slide deck
- Animate: Push slides to Notlm for animated video rendering
- Publish: Upload to YouTube; distribute PDF via email/web
- Log: Record all outputs and delivery status

TITLE PDF Report Rebrand - Design Procedure - 2. Build Stage Map

For each stage define:
- Input schema (PDF file, brand tokens, slide count)
- Output schema (rebranded PDF path, PPTX file path, Notlm job ID, YouTube URL)
- Success condition
- Failure condition
- Timeout and retry behavior

Avoid shared mutable state between stages. Each stage must produce a discrete output artifact.

TITLE PDF Report Rebrand - Design Procedure - 3. Define Node Contracts

Stage contracts:

[EXTRACT]
- Input: Raw PDF binary or URL
- Output: Structured JSON (sections, paragraphs, chart descriptions, tables)
- Failure: Unreadable PDF -> flag for manual review

[REINTERPRET]
- Input: Structured JSON from EXTRACT
- Output: Rewritten content JSON with SMAART voice, original insights, and reframed data narratives
- Failure: LLM timeout -> retry x2, fallback to draft-mode output

[REBRAND PDF]
- Input: Rewritten content JSON + brand kit
- Output: Branded PDF (cover, body, charts, footer with SMAART logo)
- Failure: Render error -> alert, hold for manual design review

[DISTILL TO PPT]
- Input: Rewritten content JSON
- Output: Slide outline JSON (title, bullet points, speaker notes per slide)
- Rule: Max 15 slides, each with one core insight, one visual placeholder

[BUILD PPT]
- Input: Slide outline JSON + brand kit
- Output: PPTX file with branded master template applied
- Failure: Template mismatch -> fallback to default branded template

[NOTLM EXPORT]
- Input: PPTX file + animation style preference
- Output: Notlm job ID, rendered video file or streaming URL
- Failure: Notlm API error -> retry x3, alert if unresolved

[PUBLISH]
- Input: Rendered video, branded PDF
- Output: YouTube URL, email/web distribution confirmation
- Failure: Upload error -> retry x2, queue for manual upload

TITLE PDF Report Rebrand - Design Procedure - 4. Engineer Reliability

Reliability controls:
- Validate PDF is readable before extraction begins
- Idempotency: tag each run with source-PDF hash to prevent duplicate outputs
- Retry with exponential backoff on LLM, render, and API calls
- Dead-letter queue for failed Notlm or YouTube publish jobs
- Manual review gate before final customer-facing PDF is distributed
- Brand compliance check: verify hex codes and logo placement before PDF render

TITLE PDF Report Rebrand - Design Procedure - 5. Add Observability

Log at each stage:
- timestamp
- workflow-name: pdf-report-rebrand
- workflow-stage
- status: success | failed | pending-review
- error-message
- output-reference (file path, URL, job ID)
- execution-time

Alerts:
- LLM reinterpret stage > 60s -> warn
- PDF render failure -> immediate alert
- Notlm job stuck > 10min -> alert
- YouTube publish failure -> alert + queue manual upload

TITLE PDF Report Rebrand - Output Format

Return outputs in this order:
1. Workflow objective and trigger
2. Stage-by-stage architecture
3. Node sequence and contracts
4. Error handling and retry policy
5. Logging and monitoring plan
6. Quality score with rationale
7. Deliverables checklist:
   - [ ] Branded PDF report (customer/employee version)
   - [ ] PowerPoint deck (employee education)
   - [ ] Notlm animated video (YouTube)
   - [ ] Distribution confirmation (email/web/portal)

TITLE PDF Report Rebrand - Validation Rule

Before finalizing, verify:
- Brand colors and logo applied to all pages
- All third-party data reinterpreted in original SMAART voice (no verbatim reproduction)
- PowerPoint slide count does not exceed 15
- Notlm job ID captured and video URL confirmed before marking complete
- YouTube video title, description, and tags align with SMAART Company content strategy
