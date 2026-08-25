## Refik Emre Soykut

Product architect at Vabers. Data analysis and research consulting since 2016.

### ODAH.AI — Statistical analysis platform for Turkish academic research

A system that takes raw survey data and produces defensible, citation-backed
statistical reports. Currently in development; source is private.

**The core constraint:** language models never generate numbers. Every
statistic, p-value and confidence interval comes from a deterministic
computation layer. The model reads context, proposes methods and writes
interpretation — it never touches the arithmetic.

---

### Engineering problems solved

**Evidence-gated measurement resolution**
Psychometric scales cannot be identified by name alone — four different
instruments in the same domain can share nearly identical titles with
different item counts. The system resolves scale identity against primary
literature: it searches, opens the source, extracts factor structure and
reverse-keyed items, then validates the claim through an independent
reviewer with its own source access. Unverified structure never enters
scoring.

**Deterministic invariant gates**
Logical consistency is not delegated to a model. If a scale has 32 items,
the union of its subscales must equal 32 — a real failure case silently
dropped one item during subscale assignment. Item coverage, overlap,
reverse-key validity, range consistency and score bounds are all checked
in code before any result is produced.

**Statistical detection cannot establish scoring keys**
Cronbach's alpha is invariant under full-scale reversal — reversing every
item yields an identical coefficient. Item-total correlation can flag a
suspicious item but cannot distinguish "reverse-keyed" from "noisy." The
system surfaces these as open questions requiring source confirmation,
never as verdicts. A published reverse-key was once discarded in favour of
a statistical one for a 0.009 gain in alpha; that path is now closed.

**Execution ledger**
Report text is bound to what actually ran. Every check and transformation
writes to a ledger — including checks that produced no findings — and the
report layer can only reference entries marked as applied. This structurally
prevents claims like "missing values were imputed" on a dataset with zero
missing cells.

**PII boundary**
Three separate channels were leaking real participant values to external
APIs: categorical column samples, identifier candidates and numeric
min/max ranges. All now pass through a single gate. Structural checks
combined with pattern heuristics keep names, emails and phone numbers
inside the system while preserving the category labels the model needs
for group naming.

**Hypothesis traceability**
Every user hypothesis is either tested or explicitly declared untestable —
none disappear silently. Operationalization is checked against data
granularity: a hypothesis about "under 30" cannot be tested when age is
banded as 25–34, and the system says so rather than substituting a proxy.

---

### Stack

Python · FastAPI · pandas · SciPy · statsmodels · React · Anthropic API

431 tests · 57-file regression corpus · deterministic snapshot verification

---

📍 Çanakkale, Turkey
