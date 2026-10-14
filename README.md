# Internet as Strategic Terrain

**An open-source intelligence platform for detecting, reconstructing, and analysing internet connectivity disruptions.**

<p align="center">
  <strong>DETECT → RECONSTRUCT → ASSESS → EXPLAIN</strong>
</p>

Internet connectivity is strategic infrastructure. When a region loses connectivity, traffic is rerouted, or access to online services is disrupted, independent measurement systems record different traces of the event.

**Internet as Strategic Terrain** combines active network probing, BGP routing data, and internet censorship measurements to investigate connectivity disruptions, reconstruct their timelines, quantify uncertainty, and evaluate what the available evidence can—and cannot—establish about their causes.

The objective is to build a reproducible intelligence-engineering platform that turns fragmented public measurements into defensible, evidence-based assessments.

---

## Project overview

| | |
|---|---|
| **Discipline** | Open-source intelligence (OSINT), network measurement, cyber intelligence |
| **Primary focus** | Internet connectivity disruptions |
| **Research approach** | Multi-source detection, event reconstruction, statistical evaluation |
| **Data policy** | Publicly available measurement data and documented sources |
| **Reproducibility** | Versioned datasets, repeatable pipelines, documented methodology |
| **Version 1.0** | Day 90 — validated research pipeline |
| **Version 2.0** | Day 107 — interactive command-center console |

### Research question

> Can independent internet measurement sources be combined to detect, reconstruct, and characterise connectivity disruptions more reliably than any individual source?

This project tests that question empirically rather than assuming that combining more data automatically produces better intelligence.

The evaluation compares individual measurement sources against a multi-source approach, using historical events, documented ground truth where available, and uncertainty-aware performance metrics.

## Objectives

- **Detect:** Identify abnormal connectivity conditions using measurable signals.
- **Reconstruct:** Establish the likely onset, duration, geographic scope, and evolution of an event.
- **Correlate:** Determine whether independent measurement sources support, contradict, or fail to corroborate one another.
- **Assess:** Quantify detection performance, uncertainty, data coverage, and evidential limitations.
- **Explain:** Develop evidence-based hypotheses about possible causes without confusing correlation with attribution.
- **Reproduce:** Make the analytical process repeatable from raw observations to final assessment.
- **Generalise:** Build reusable components that can support future investigations into other strategic infrastructure and geopolitical events.

## Initial case study: Kherson, Ukraine — 30 May 2022

The first investigation examines the reported connectivity outage and rerouting associated with Kherson on 30 May 2022.

The case will be assessed against independently published reporting, including relevant material from Cloudflare and WIRED, alongside available technical measurements.

### Investigation workflow

1. Establish the reported event timeline and identify source documents.
2. Locate relevant historical network measurements and assess their coverage.
3. Identify anomalies in connectivity and routing behaviour.
4. Correlate observations across independent data sources.
5. Reconstruct the event timeline and characterise its observable impact.
6. Compare the resulting assessment with published reporting.
7. Document uncertainty, competing explanations, and unresolved questions.

**Fallback case:** If historical coverage for Kherson is insufficient, investigate the 2011 connectivity disruptions in Egypt or Libya, drawing on the events examined in the foundational Dainotti et al. research.

The fallback decision will be based on data availability, measurement quality, and the ability to evaluate the methodology—not on which event produces the most compelling narrative.

## Data sources

The initial research will investigate three complementary measurement categories.

| Source | What it can reveal | Important limitation |
|---|---|---|
| **Active network probing** | Reachability changes, probe failures, and differences in observed connectivity | Probe coverage is incomplete and failures may have causes unrelated to a regional outage |
| **BGP routing measurements** | Route withdrawals, announcement changes, and shifts in routing visibility | A routing change does not necessarily mean end users have lost connectivity |
| **Censorship measurements** | Changes in the accessibility of particular services, domains, or protocols | Blocking of a service is not equivalent to a complete internet outage |

Candidate datasets, collection periods, licensing conditions, and geographic coverage will be documented before implementation. Availability of historical observations will be verified during the initial research phase.

## Analytical methodology

### 1. Data acquisition and validation

- Identify relevant public datasets and measurement APIs.
- Record source provenance, collection timestamps, geographic coverage, and limitations.
- Validate schemas, timestamps, missing values, and duplicate observations.
- Preserve raw data separately from transformed datasets.
- Track data availability and ingestion failures.

### 2. Event detection

Establish normal measurement behaviour where sufficient historical data exists, then identify deviations that may indicate a disruption.

Candidate signals include:

- Abnormal increases in probe failures.
- Changes in BGP announcements and withdrawals.
- Changes in observed reachability or routing visibility.
- Deviations from historical patterns and relevant comparison regions.

Detection thresholds and baseline periods will be documented and tested for sensitivity.

### 3. Multi-source correlation

Align observations by time and, where defensible, by network, region, or affected service.

Evaluate whether independent signals:

- Occur within a consistent time window.
- Indicate compatible forms of disruption.
- Expand or narrow the estimated event scope.
- Provide genuinely independent corroboration or share underlying measurement dependencies.

The analysis will distinguish missing evidence from evidence that contradicts a hypothesis.

### 4. Event reconstruction

Generate a structured event record containing, where supported:

- Estimated start and end times.
- Detection and recovery intervals.
- Affected networks, regions, or services.
- Observed routing changes.
- Supporting and conflicting measurements.
- Confidence estimates and known data gaps.

When exact onset or recovery cannot be established, report an interval rather than inventing a precise timestamp.

### 5. Evidence assessment

Every significant analytical claim should be traceable to its underlying measurements or documented sources.

The assessment will distinguish:

- **Observation:** What the measurements directly show.
- **Inference:** What follows from the observations under stated assumptions.
- **Hypothesis:** A possible explanation requiring additional evidence.
- **Attribution:** A claim about responsibility or cause requiring evidence beyond the existence of a disruption.

The presence of an outage and the identity or intent of the actor responsible are separate analytical questions.

## Evaluation framework

The core contribution is not simply detecting a historical outage. It is testing whether multi-source analysis improves the quality of detection and reconstruction.

The evaluation will compare:

1. Active probing alone.
2. BGP routing measurements alone.
3. Censorship measurements alone, where applicable.
4. A combined multi-source approach.

Candidate metrics include:

| Metric | Purpose |
|---|---|
| Precision | How often detected events correspond to validated events |
| Recall | How many validated events are detected |
| F1 score | Balance between precision and recall |
| Detection delay | Time between the earliest defensible event onset and detection |
| Timeline error | Difference between estimated and reference event times |
| Geographic or network coverage | How much of the documented event can be characterised |
| Calibration | Whether stated confidence levels correspond to observed reliability |
| Uncertainty intervals | How much uncertainty remains in event timing and scope |

Metrics will only be reported when the data supports their calculation. The evaluation will document reference-label quality, class imbalance, missing data, and potential leakage between training, calibration, and test periods.

Where feasible, confidence intervals will quantify uncertainty in performance estimates. A single historical case will be treated as a case study, not proof of general performance across all disruptions.

## Technical architecture

The project will evolve from a reproducible research pipeline into an interactive analytical interface.

```text
             PUBLIC MEASUREMENT SOURCES
          ┌──────────┬──────────┬──────────┐
          │  Active  │   BGP    │Censorship│
          │  Probing │ Routing  │  Data    │
          └────┬─────┴────┬─────┴────┬─────┘
               └──────────┼──────────┘
                          ▼
                INGESTION & VALIDATION
                          │
                          ▼
                  NORMALISED DATA
                          │
                          ▼
                 TEMPORAL CORRELATION
                          │
                          ▼
                 EVENT DETECTION
                          │
                          ▼
                EVENT RECONSTRUCTION
                          │
                          ▼
                EVIDENCE & UNCERTAINTY
                          │
                          ▼
                  EVALUATION REPORTS
                          │
                          ▼
                 COMMAND-CENTER UI
                       (v2.0)
```

The architecture will be refined as the source inventory and data requirements become clear. Technology choices will follow demonstrated requirements rather than adding infrastructure for its own sake.

## Development roadmap

The build plan uses three focused tasks per day, approximately 30–60 minutes of total daily work, and a buffer day at the end of each phase.

The schedule is a target, not a substitute for validation. If a dataset or methodological assumption proves inadequate, the plan should adapt rather than conceal the limitation.

### Version 1.0 — Day 90

**Deliverable: a reproducible research and evaluation pipeline.**

- [ ] Define the research question, scope, and evaluation criteria.
- [ ] Identify and validate the initial public measurement sources.
- [ ] Establish the historical event reference timeline.
- [ ] Build repeatable ingestion and validation workflows.
- [ ] Normalise measurements and align observations temporally.
- [ ] Implement individual-source detection baselines.
- [ ] Implement multi-source correlation and event reconstruction.
- [ ] Quantify uncertainty and evaluate detection performance.
- [ ] Produce an evidence-linked case study and research report.
- [ ] Document setup, data provenance, limitations, and reproduction steps.

**Release criterion:** Version 1.0 is complete when another person can follow the documented workflow, reproduce the analysis from accessible data, inspect the evidence behind the findings, and understand the limitations of the conclusions.

### Version 2.0 — Day 107

**Deliverable: an interactive intelligence command-center console.**

- [ ] Design an event-centric analytical interface.
- [ ] Visualise disruption timelines and affected networks or regions.
- [ ] Display correlated signals from the available measurement sources.
- [ ] Surface evidence provenance and uncertainty alongside findings.
- [ ] Add event filtering, investigation summaries, and source drill-downs.
- [ ] Connect the interface to the validated analytical outputs.
- [ ] Document the console architecture and demonstrate the historical case.

The console is a presentation and investigation layer, not a replacement for the underlying evidence pipeline.

## Repository structure

The following is a proposed structure; directories will be added as implementation progresses.

```text
internet-as-strategic-terrain/
├── README.md
├── docs/
│   ├── research-question.md
│   ├── methodology.md
│   ├── data-sources.md
│   ├── evaluation.md
│   └── case-studies/
│       └── kherson-2022.md
├── configs/
├── data/
│   ├── raw/
│   ├── processed/
│   └── reference/
├── notebooks/
├── src/
│   ├── ingestion/
│   ├── validation/
│   ├── normalisation/
│   ├── detection/
│   ├── correlation/
│   ├── reconstruction/
│   └── evaluation/
├── tests/
├── reports/
└── dashboard/
```

Large datasets, restricted data, credentials, and generated artifacts should not be committed to Git. The repository should contain source references, data acquisition instructions, reproducible code, and small example fixtures where permitted.

## Responsible analysis

Internet measurements are incomplete, and technical observations rarely establish intent on their own.

This project will therefore:

- Use public, lawfully accessible measurement sources.
- Respect source licensing, access policies, and applicable terms.
- Avoid collecting unnecessary personal or sensitive information.
- Distinguish confirmed observations from interpretations and hypotheses.
- Document missing coverage and alternative explanations.
- Avoid presenting a correlation as proof of causation or responsibility.
- Preserve uncertainty rather than forcing every event into a definitive narrative.

The objective is defensible analysis, not the appearance of certainty.

## Research foundations

The initial investigation will build on established work in internet measurement, censorship detection, routing analysis, and the study of large-scale connectivity disruptions.

Key starting points:

- **Dainotti et al.** — *Analysis of Country-wide Internet Outages Caused by Censorship*, an important foundation for studying large-scale national connectivity disruptions.
- **Cloudflare** — Internet traffic, connectivity, and outage reporting that may help establish context for the selected event.
- **WIRED** — Published reporting relevant to the Kherson case and its historical context.

Exact publications, source URLs, relevant passages, and the role each source plays in validating the event will be recorded in the case-study documentation. Published reporting will serve as reference evidence, not as a substitute for independent measurement analysis.

## Project principles

**Evidence before narrative.** Establish what happened before proposing why it happened.

**Independent corroboration.** Test whether multiple sources improve the assessment rather than assuming they do.

**Uncertainty is a result.** Incomplete coverage and ambiguous signals are part of the analytical output.

**Reproducibility over spectacle.** Every conclusion should be traceable to a documented process.

**Reusable infrastructure.** Build components that can support future investigations into other strategic systems without rebuilding the analytical foundation.

---

*Internet as Strategic Terrain — Version 1.0 target: Day 90. Command-center console: Day 107.*

**Detect the disruption. Reconstruct the event. Assess the evidence. Explain what can be established.**
