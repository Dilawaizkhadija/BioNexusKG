# Current Project Audit — BioNexusKG

**Audit date:** <FILL IN: e.g. 2026-07-05>
**Auditor:** Dilawaiz Khadija
**Repository audited:** https://github.com/Dilawaizkhadija/BioNexusKG (main, commit <FILL IN commit hash>)
**Purpose:** Establish the *actual, verifiable* state of the repository before starting
the reproducible BioNexusKG-Lite v1.0 rebuild. This document separates what exists in
code and data from what is currently only described in text.

---

## 1. Method

The audit was performed by inspecting the repository file tree, the language statistics
reported by GitHub, and the README. A claim is marked **Verified** only if there is a
file, dataset, log, or runnable script in the repository that supports it. Claims that
appear only in prose (README, report) are marked **Unverified — needs evidence**.

---

## 2. What the repository actually contains

| Item | Present in repo? | Evidence |
|------|------------------|----------|
| React + D3 demo application | Yes | `src/`, `public/`, `package.json`; language stats show JS 94.2%, HTML 3.8%, CSS 2.0% |
| README describing the project | Yes | `README.md` |
| Python data pipeline code | **No** | 0% Python in language stats; no `.py` files in tree |
| `pipeline/` folder (harvest/resolve/ingest) | **No** | Not present in file tree (README lists it, but it is not committed) |
| Neo4j database / dump / import scripts | **No** | No `.cypher`, no `neo4j/` folder, no dump file |
| Harvested raw data (JSON/TSV) | **No** | No `data/` folder |
| Processed graph files (CSV/Parquet/RDF exports) | **No** | No `exports/` folder |
| KG embeddings (PyKEEN) | **No** | No embedding files, no training script or logs |
| Validation code or result logs | **No** | No `validation/` folder, no metric output files |
| `docker-compose.yml` | **No** | Not present in file tree |

**Summary:** The repository is a **static front-end demonstration**. It renders
hardcoded / illustrative sample data. No live data pipeline, graph database, embedding
model, or validation procedure currently exists in the repository.

---

## 3. Numbers displayed by the demo (status: illustrative, not measured)

The following figures appear in the README and demo. They are labelled with "Est." or
"~" in the source and have **no supporting dataset or log in the repository**. They are
therefore treated as **placeholder / illustrative values**, not results.

- 12 data sources
- 12 node types
- 22 relationship types
- ~107,000 nodes
- ~1,070,000 edges
- Link prediction: TransE Hits@10 = 0.78, ComplEx MRR = 0.42
- Drug repurposing AUROC = 0.87
- Gold-standard Precision@100 = 0.91
- Expert panel agreement = 85%
- Cross-DB Jaccard = 0.72

None of these will be repeated as facts anywhere in the rebuilt project until they can be
regenerated from committed code and data.

---

## 4. Minor accuracy issues found

- The sample edge in the README references `clinicaltrials.gov/ct2/show/NCT...`, which is
  the **retired classic URL format**. The live ClinicalTrials.gov API is v2
  (`clinicaltrials.gov/api/v2/studies`); the classic API was retired in June 2024. This
  confirms the metadata was written by hand rather than retrieved from the live source.
- The README "Project Structure" section documents folders (`pipeline/`, `embeddings/`,
  `exports/`) that are not committed. The documentation currently describes an intended
  design as if it were implemented.

---

## 5. Honest conclusion

BioNexusKG today is a **well-presented demo of a knowledge graph that has not yet been
built**. This is a valid and useful starting point, but it is not yet a reproducible
research artifact. Week 1 of the rebuild converts the project from "described" to
"reproducible-in-progress" by fixing scope, schema, and documentation first.
