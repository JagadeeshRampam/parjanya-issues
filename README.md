# Parjanya — Issue Tracker

Welcome! This is the public home for **Parjanya 2.0** — the AI-assisted
photography curation platform by [Phagyul AI Systems](https://blog.phagyul.ai) —
where you can report bugs, request features, follow known issues, and read
release notes.

- 🐛 **Found a bug?** [Open a bug report](../../issues/new?template=bug_report.yml)
- 💡 **Have an idea?** [Request a feature](../../issues/new?template=feature_request.yml)
- 📋 **Known issues** are labelled [`known-issue`](../../issues?q=is%3Aissue+is%3Aopen+label%3Aknown-issue)
- 📦 **Release notes** live under [Releases](../../releases)

Please search existing issues before filing a new one. Don't include account
credentials or personal data in reports — screenshots of the UI are fine.

---

## What happens to your photos

Parjanya is built for working photographers who come back from a shoot with
thousands of frames. Here's the journey every image takes:

```
 1. Upload      Your RAW/JPEG files (34 formats, up to 500MB each) go straight
                to secure cloud storage — resilient to network drops and pauses.
 2. Extract     Camera metadata (EXIF) is read and fast web previews are
                generated, so your gallery is browsable within moments.
 3. Screen      A technical pass catches exact duplicate re-uploads and groups
                rapid-sequence (burst) shots so near-identical frames don't
                flood your gallery.
 4. Enrich      A vision AI studies each image — distortion types (blur, noise,
                exposure issues) with severity, plus rich descriptions that
                power search.
 5. Verdict     A rule engine turns that analysis into Accept / Review /
                Reject — based on what's wrong and how badly, never an opaque
                score.
 6. You decide  Override any verdict with one click. Your corrections are
                remembered and will personalise future curation to your taste.
```

You can watch costs and storage for all of this on the in-app **Usage &
Costs** dashboard.

## Why your batch never silently stalls

Behind the scenes, Parjanya treats reliability as a first-class feature. The
platform is designed around the **TBIE model** — **Truth, Belief, Intent,
Execution**:

- **Truth** — the durable record of your images and where each one is in its
  journey. It survives any crash.
- **Belief** — what the system *thinks* is happening right now (queue depths,
  worker health). Useful, but never blindly trusted.
- **Intent** — a durable declaration of what should happen next to each image.
- **Execution** — the disposable machinery (serverless functions, GPU workers)
  that does the work, built so it can be safely restarted and re-run.

A **reconciliation loop** continuously compares Truth against Intent: if any
image's journey stalls at any stage — a transient failure, a lost message, a
worker interruption — the divergence is detected and that exact step is
automatically replayed. Intermittent failures self-heal; genuine errors are
caught, bounded, and surfaced rather than retried forever. In our 450GB /
12,000-image validation run, this loop repaired thousands of stalled records
with zero manual intervention.

Want the engineering deep-dive? Read
[**From Pipeline to Platform**](https://blog.phagyul.ai/p/from-pipeline-to-platform)
— how the replay engine "stopped being a utility [and] became the control
plane" — and its companion piece, *TBIE in Practice: Designing Resilient AI
Pipelines That Recover, Reconcile, and Re-run*.

## Roadmap

Where the platform is heading — tracked as issues labelled
[`roadmap`](../../issues?q=is%3Aissue+is%3Aopen+label%3Aroadmap) so you can
follow, vote (👍), and comment:

- **[Fair-share dispatcher — control-plane scheduling](../../issues/10)** —
  guaranteed per-tenant throughput shares, batch pause/resume, priorities,
  and accurate batch ETAs. *(Shipped precursor, 2026-07: per-tenant fair
  scheduling — one tenant's bulk batch can no longer starve another tenant's
  fresh upload.)*
- **[Deduplication](../../issues/4)** — exact-duplicate detection is live;
  near-duplicate matching (burst-aware, review-first) is next — the issue
  tracks implementation status and history
- **[Semantic search](../../issues/11)** — keyword search over AI
  descriptions works today; true meaning-based search (embeddings) is
  planned — the issue has the fix plan and current status
- **[Personalized curation from your overrides](../../issues/5)**
- **[Composition-aware enrichment](../../issues/6)**
- **[In-app notifications](../../issues/8)**
- **[Self-serve payments](../../issues/9)**

## What we're working on now

Work is grouped into sprint milestones. Follow along, or filter any list by milestone:

- [**Sprint 1: Ship and close**](../../milestone/1): ship what is built, confirm fixes that are waiting on a live event, settle open decisions
- [**Sprint 2: Correctness and customer-visible gaps**](../../milestone/2): search, upload edge cases, burst and duplicate handling, notifications
- [**Sprint 3: Cost and performance**](../../milestone/3): storage and request volume, GPU cold start, caching

The carry-over list behind these is [#133](../../issues/133). Open problems we know about stay under [`known-issue`](../../issues?q=is%3Aissue+is%3Aopen+label%3Aknown-issue); each shows a status label (`planned`, `in progress`, `verifying`, `waiting`) that moves as the work does.

## R&D and behind-the-scenes

The [Phagyul AI Systems blog](https://blog.phagyul.ai) covers the research,
field notes, and behind-the-scenes engineering of our products — Parjanya
v2.0, WilderhoodTV, and Smriti LLM. If you want to know *why* the platform
works the way it does, that's the place.
