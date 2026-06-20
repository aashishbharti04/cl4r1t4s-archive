# Generational diff — Claude Opus 4.7 → Claude Fable 5

Comparing two extractions from `elder-plinius/CL4R1T4S/ANTHROPIC/`:

| | File | Lines | Captured (injected date) |
|---|---|---|---|
| Older | `Claude-Opus-4.7.txt` | 1,408 | Thursday, April 16, 2026 |
| Newer | `CLAUDE-FABLE-5.md` | 1,597 | Tuesday, June 09, 2026 |

Both are the **consumer claude.ai** system prompt (same toolset: places, recipes, sports,
image search), so this is a like-for-like generational comparison. Format differs
cosmetically — 4.7 uses `{section}`/`{/section}` tags, Fable 5 uses `##` markdown headers.

---

## 1. `product_information` — the concrete factual changes

| Field | Opus 4.7 | Fable 5 |
|---|---|---|
| This model | "Claude Opus 4.7, from the Claude 4.7 family… most advanced and intelligent model currently available" | "Claude Fable 5, first model in the **Claude 5** family, part of a new **Mythos-class** tier that sits **above Opus**" |
| Sibling model | — | **Claude Mythos 5** — same underlying model, fewer dual-use safeguards, approved orgs only |
| "Most recent" list | Opus 4.7, Opus 4.6, Sonnet 4.6, Haiku 4.5 | Fable 5, **Opus 4.8**, Sonnet 4.6, Haiku 4.5 |
| Model strings | `claude-opus-4-7`, `claude-opus-4-6`, `claude-sonnet-4-6`, `claude-haiku-4-5-20251001` | `claude-fable-5`, `claude-opus-4-8`, `claude-sonnet-4-6`, `claude-haiku-4-5-20251001` |
| Products | Claude Code (terminal only); Chrome, Excel, **Cowork** | Claude Code (**terminal + desktop + mobile**); Chrome, Excel, **PowerPoint** (new), Cowork (promoted to "agentic knowledge-work app") |
| Dedicated link | — | `anthropic.com/news/claude-fable-5-mythos-5` |

Net: Opus stepped 4.7 → 4.8 and dropped below the new Mythos tier; Sonnet/Haiku unchanged;
**Claude in PowerPoint** is newly added; Claude Code's reach expanded to desktop/mobile.

`knowledge_cutoff` is **end of Jan 2026 in both** — the cutoff did not move between generations;
only the per-conversation injected "today" date differs (Apr 16 → Jun 9), which also tells us
roughly when each prompt was captured.

---

## 2. Sections REMOVED in Fable 5 (present in 4.7, gone now)

- **`default_stance`** — 4.7's explicit "Claude defaults to helping; only declines when helping
  would create a concrete, specific risk of serious harm" block. **Dropped** as a standalone
  framing in Fable 5 (refusal posture is now distributed across `refusal_handling`).
- **`tool_discovery`** — 4.7's whole section on deferred tools / `tool_search` ("the visible tool
  list is partial by design… search for tools before assuming you lack a capability"). **Gone.**
- **`past_chats_tools`** — 4.7's dedicated past-conversation retrieval section. **Gone** (Fable 5
  keeps only the short `memory_system` block).
- **Inline visualizer** — 4.7's `when_to_use_visualizer_for_inline_visuals` +
  `visualizer_examples` (19 references). **Removed entirely** in Fable 5.
- **`search_first`** — 4.7 leads `claude_behavior` with a prominent standalone "search before
  EVERY factual question" block. Fable 5 has no such top-level block; that behavior is folded
  into `knowledge_cutoff` and `search_instructions`.
- Minor: 4.7's `unnecessary_computer_use_avoidance`, `notes_on_user_uploaded_files`, and
  `request_evaluation_checklist` are absorbed into other sections rather than standing alone.

## 3. Sections ADDED / expanded in Fable 5

- **`mcp_app_suggestions`** (NEW section) — the `[third_party_mcp_app]` connector etiquette:
  directory-first, `search_mcp_registry` → `suggest_connectors`, opt-in before calling consumer
  partners, "never pick a partner for someone who didn't ask." Note: the connector *tools*
  (`search_mcp_registry`, `places_search`) already existed in 4.7; what's new is the dedicated
  behavioral playbook around them.
- **`critical_child_safety_instructions`** — expanded with rules absent in 4.7: not decoding
  CSAM slang even while refusing; staying at "pattern level" for protective content; stating the
  principle rather than the detection mechanics.
- **`user_wellbeing`** — several new paragraphs vs 4.7: no naming an undisclosed diagnosis;
  no causal narratives for disordered eating; handling a past bad experience with crisis services
  without totalizing; the anti-over-reliance / "never thank the person for reaching out" rule.
- **`evenhandedness`** — tightened wording; new "charity applies to the topic, not every
  requested format" point (can decline a forced yes/no on contested issues).
- **Explicit `Tool Definitions` block** — Fable 5 dumps fuller JSON-schema tool definitions under
  one header, including `recommend_claude_apps` and `weather_fetch`.

## 4. Sections essentially UNCHANGED across both

`persistent_storage_for_artifacts` (storage API), `legal_and_financial_advice`,
`anthropic_reminders` (same reminder set), `responding_to_mistakes_and_criticism`,
`CRITICAL_COPYRIGHT_COMPLIANCE` (same 15-word / one-quote hard limits),
`harmful_content_safety`, `citation_instructions`, the `anthropic_api_in_artifacts`
("Claudeception") section, and `network_configuration`. The NEDA → National Alliance for
Eating Disorders redirect is present in both.

---

## 5. Carry-over staleness worth flagging

The `anthropic_api_in_artifacts` ("Claudeception") example still hardcodes
`model: "claude-sonnet-4-20250514" // Always use Sonnet 4` in **both** 4.7 and Fable 5 — i.e.
the May-2025 Sonnet 4 ID, which contradicts each prompt's own "current models" list. This is a
long-lived stale spot that survived the generation bump, not a one-off extraction error. Anyone
lifting that snippet should swap in `claude-sonnet-4-6`.

---

## Headline takeaways

1. **Capability story:** new top tier (Mythos-class: Fable 5 / Mythos 5) lands above Opus, which
   itself ticks 4.7 → 4.8. Sonnet/Haiku held steady. Knowledge cutoff held at Jan 2026.
2. **Biggest behavioral shift:** the explicit `default_stance` "default to helping" block was
   removed, and the `search_first` mandate was demoted from a headline rule to distributed
   guidance — both suggesting a re-tuning of how aggressively those postures are asserted.
3. **Feature churn:** inline visualizer and the deferred-tool / past-chats framing dropped;
   MCP-connector suggestion etiquette and Claude-in-PowerPoint added.
4. **Safety sections grew:** child-safety and wellbeing both gained materially more specific rules.
