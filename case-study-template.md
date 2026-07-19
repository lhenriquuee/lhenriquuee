# Case study template

Use this structure for each sample in `case-studies/`. It shows *process*,
which is what differentiates a Technical Writer from someone who can just
write clean sentences.

---

## [Document title]

**Context:** One or two sentences — what product/feature this documents, and
who the audience is (end users, developers, support team...).

**Problem:** What was missing or unclear before this documentation existed?
(e.g. "Users were opening support tickets to ask how to register a PIX key
because there was no self-service guide.")

**Process:**
- Who did you talk to (SMEs, product, support) to gather information?
- What tool did you use (Markdown/VS Code, Jira for tracking, etc.)?
- Any constraints (deadline, technical complexity, translation needs)?

**Result:** What changed after the doc was published? Use a number if you
have one (e.g. "reduced related support tickets by X%," "adopted as the
default onboarding guide for Y team"). If you don't have metrics, describe
the outcome qualitatively — e.g. "adopted as the standard reference for the
onboarding flow."

**Sample:** [Link to the actual document, or paste an excerpt below]

```markdown
<!-- Excerpt of the actual documentation goes here -->
```

---

### Example (filled in)

## How to Register a PIX Key

**Context:** Step-by-step guide for end users registering a PIX key inside
the app, aimed at non-technical users.

**Problem:** Support was getting repeated tickets about PIX key registration
with no existing self-service documentation to deflect them.

**Process:** Interviewed the support team to identify the most common points
of confusion, tested the flow myself, and wrote the guide in Markdown,
version-controlled in GitHub.

**Result:** Reduced related support tickets and became the go-to reference
linked directly from the support team's macros.

**Sample:** [register-a-pix-key.md](../how-to-guides/register-a-pix-key.md)
