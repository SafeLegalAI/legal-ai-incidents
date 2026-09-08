---
license: cc-by-4.0
pretty_name: "SafeLegalAI Legal AI Incident Tracker"
language:
  - en
multilinguality:
  - monolingual
annotations_creators:
  - expert-generated
language_creators:
  - found
source_datasets:
  - original
size_categories:
  - n<1K
tags:
  - legal
  - law
  - ai-safety
  - hallucination
  - courts
  - sanctions
  - professional-responsibility
  - generative-ai
  - safelegalai
configs:
  - config_name: incidents
    default: true
    data_files:
      - split: train
        path: data/incidents.jsonl
---

# SafeLegalAI Legal AI Incident Tracker

**What went wrong when AI met the courtroom, and what did courts and regulators do about it?**

150 incidents · 15 jurisdictions · 48 with a recorded regulatory outcome · last checked 2026-09-05 · synced from [safelegalai.com](https://safelegalai.com) on 2026-09-08.

Every court case where AI misuse reached a judgment or order: the court, the date, what was fabricated or misused, the outcome, any penalty, who the actor was, and — the layer no other tracker keeps — what the professional regulator did next. Every record links its primary source (judgment, order or regulator notice).

This is a mirror. The canonical, always-current version lives at **[safelegalai.com/tracker](https://safelegalai.com/tracker)**, where every record has a permanent page, a citation block and its last-checked date; the JSON served there ([/tracker/incidents.json](https://safelegalai.com/tracker/incidents.json)) is the source of this repository. Each row's `url` field points to its record page. The same files are mirrored on GitHub at [github.com/SafeLegalAI/legal-ai-incidents](https://github.com/SafeLegalAI/legal-ai-incidents) (issues welcome there).

## Tables

| config | rows | what a row is | files |
|---|---|---|---|
| `incidents` | 150 | one row per court decision where AI misuse was found | [`data/incidents.jsonl`](data/incidents.jsonl) · [`csv/incidents.csv`](csv/incidents.csv) |

## Fields

| field | meaning |
|---|---|
| `id` | stable slug; the record page is `url` |
| `caseName` · `court` · `date` · `jurisdiction` | the decision; `jurisdiction` is the tracker bucket (uk, us-federal, us-state, eu, india…) |
| `aiTool` | only when the record names it; otherwise absent — never guessed |
| `conduct` | what was hallucinated, fabricated or misused |
| `outcome` · `monetaryPenalty` · `penaltyCurrency` | sanctions · fine · costs-order · referral · warning · strike-off · suspension · dismissal · pending · other |
| `actor` | lawyer · litigant-in-person · prosecutor · judge · expert · firm · other |
| `regulatoryOutcome` | `{body, disposition, date}` — what the SRA, BSB, state bar, law society… did after the court |
| `sources` | `[{label, url}]`, primary source first |
| `summary` | 40–60 words, self-contained |
| `status` | verified · unverified (flagged, never silently included) |
| `relatedRegulations` · `article` | slugs into the regulation dataset and the analysis article, if any |
| `lastVerified` | date the record was last re-opened against its sources |

Dates are `YYYY-MM-DD`. Optional fields are absent (JSONL) or empty (CSV) when unknown — nothing is guessed. In the CSV, arrays of scalars are joined with `; ` and nested objects are JSON strings.

## Method

We record findings made by courts and regulators; we do not make them. Every record links a primary source (judgment, order, regulator notice, official document or vendor page) and carries the date it was last re-opened against that source. Unverified records are flagged `unverified`, never silently included. Inclusion criteria, the correction process and the ownership/funding disclosure are published at [safelegalai.com/editorial-standards](https://safelegalai.com/editorial-standards); every content run is logged at [safelegalai.com/changelog](https://safelegalai.com/changelog).

## Use

```python
from datasets import load_dataset
ds = load_dataset("safelegalaidata/legal-ai-incidents")
```

## Cite

> SafeLegalAI (published by Cognesio LLP), "Legal AI Incident Tracker", safelegalai.com, accessed 2026-09-08. https://safelegalai.com/tracker — data: CC BY 4.0.

Cite the primary source as the authority and this dataset as the structured record that surfaced it. Corrections and right of reply: [safelegalai.com/report](https://safelegalai.com/report).

## Licence

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribution: **SafeLegalAI (safelegalai.com), published by Cognesio LLP** with a link to https://safelegalai.com/tracker. Primary sources keep their own licences and copyright.

## Disclaimer and notices

**Provided "as is", without warranty of any kind** — the CC BY 4.0 licence excludes all warranties and limits liability (section 5), and those exclusions apply to this dataset. **Not legal advice**; no lawyer–client relationship arises from using it. Cognesio LLP is not a law firm. SafeLegalAI records findings made by courts, regulators and vendors' own published pages; it makes no findings of its own, and the linked official documents are the record. Editorial classifications (status labels, requirement codes, "documented yes/no/not disclosed") are opinions about documents, expressed in good faith; the document prevails. Where a row names a person or organisation, it does so as they appear in a public court document, official publication or their own published material — a fair and accurate report published in good faith and in the public interest; anyone named may reply or request a correction at https://safelegalai.com/report. Product, company, court and regulator names and marks belong to their owners and identify the product or body referred to; no affiliation or endorsement is implied. Full terms, notice-and-takedown and governing law (England and Wales): https://safelegalai.com/disclaimer.

## Related datasets

- [Legal AI Regulation Map](https://huggingface.co/datasets/safelegalaidata/legal-ai-regulation-map) — canonical page https://safelegalai.com/regulation
- [Legal AI Regulation Documents (versioned)](https://huggingface.co/datasets/safelegalaidata/legal-ai-regulation-documents) — canonical page https://safelegalai.com/regulation/documents
- [Legal Tech Tools — governance facts](https://huggingface.co/datasets/safelegalaidata/legal-ai-tools) — canonical page https://safelegalai.com/tools
- [All datasets and what is in preparation](https://safelegalai.com/datasets)

## Manifest

```json
{
  "dataset": "SafeLegalAI Legal AI Incident Tracker",
  "canonical": "https://safelegalai.com/tracker",
  "source": "https://safelegalai.com/tracker/incidents.json",
  "catalogue": "https://safelegalai.com/datasets",
  "publisher": "Cognesio LLP",
  "license": "CC BY 4.0",
  "licenseUrl": "https://creativecommons.org/licenses/by/4.0/",
  "lastChecked": "2026-09-05",
  "synced": "2026-09-08",
  "notice": "Provided as is, without warranty; not legal advice. SafeLegalAI records findings made by courts, regulators and vendors' own pages; the linked official documents are the record. Names and marks belong to their owners. Terms: https://safelegalai.com/disclaimer",
  "tables": {
    "incidents": 150
  },
  "contentSha256": "eec665689df3378ae6926e569a9cb851d3be763820450459160c5fe859919b3c"
}
```
