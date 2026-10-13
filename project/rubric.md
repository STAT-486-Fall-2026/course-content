# STAT 486 Research Project Rubric

The [project brief](README.md) is the source for requirements, dates, and submissions. The **100 project points** are divided among checkpoints (30), reproducible workflow (20), presentation (20), and written report (30). A thoughtful negative result can earn full credit. Model count, compute spent, and competition rank do not earn points by themselves.

## Checkpoints: 30 points

Checkpoint points reflect the dated README entry and linked evidence reasonably available on that date. The final artifact is judged on its final state, so a checkpoint weakness is not counted twice.

| Checkpoint | Points | What earns the points |
| --- | ---: | --- |
| Team and directions | 3 | A functioning team and repository; two feasible questions with plausible data and room for investigation. |
| Project plan | 6 | A focused question, feasible data and route-specific plan, an evaluation idea that could challenge the team's claim, and a workable fallback. |
| Data and reference result | 6 | Traceable data, a defensible evaluation plan, and a runnable first result or baseline that the team can explain. |
| Working investigation | 5 | A functioning new component (A), valid Kaggle submission pipeline (B), or source-to-clean-data pipeline with initial ML result (C); an informative first check and a clear next question. |
| Evidence and interpretation | 5 | Meaningful results, attention to a failure or limitation, and a reasoned interpretation or adjustment. For B, explain the change between pipelines and any improvement or degradation observed so far. |
| Reproduction draft | 5 | The December 3 draft includes the main code and results, committed `uv` environment files, and clear README setup and run instructions. B teams link two valid Kaggle submissions, one from each pipeline, and the commands that generated them. A reader can identify the main result and known gaps. |
| **Total** | **30** |  |

## Reproducible workflow: 20 points

| Criterion | Points | Strong work demonstrates |
| --- | ---: | --- |
| Working route-specific pipeline | 8 | The team's method or pipeline runs from documented inputs to a meaningful ML result and implements the route's central contribution competently. |
| Environment and run instructions | 6 | The repository includes `pyproject.toml` and `uv.lock`; a fresh clone can run `uv sync` and the documented `uv run` command. The README explains setup and run order. |
| Data and result traceability | 6 | Data provenance and access are clear, important quality or validity checks are present, and the reported result can be traced to code, configuration, and saved outputs. |
| **Total** | **20** |  |

For **A**, the working pipeline includes the team's new component and a suitable reference. For **B**, two meaningfully different, documented pipelines each run from competition data to a valid submission; their configurations, commands, and results make the design change testable. For **C**, the repository includes the scraping or collection scripts used for the reported dataset, builds or verifies the cleaned dataset from permitted inputs, and feeds that dataset into ML. All three routes can earn the full workflow score without a novel estimator.

## Presentation: 20 points

Use the [presentation scoring sheet](presentation-rubric.md) for the detailed, item-by-item assessment during each talk.

| Criterion | Points | Strong work demonstrates |
| --- | ---: | --- |
| Project story | 5 | The question, motivation, route, and main choices are easy to follow. |
| Work and evidence | 7 | The team explains what it built or tried and uses appropriate results, comparisons, or examples to support the main claims. B teams explain the change between pipelines and whether results improved or degraded. |
| Outcomes and reflection | 5 | The talk explains the final outcome, an important challenge or limitation, and what the team learned. |
| Delivery and participation | 3 | Visuals or demonstration are clear, the talk fits the allotted time, all members contribute, and questions are answered thoughtfully. |
| **Total** | **20** |  |

## Written project report: 30 points

| Criterion | Points | Strong work demonstrates |
| --- | ---: | --- |
| Motivation and project path | 8 | The completed `report.md` explains why the team chose the question and recounts the main steps, data, and ML work in a way a new reader can follow. |
| Challenges and decisions | 8 | The team describes meaningful obstacles, tradeoffs, changes of plan, and its reasons for important decisions. |
| Outcomes and evidence | 10 | Final results are linked to relevant figures, tables, or outputs; evaluation fits the question; conclusions and limitations match the evidence. For B, compare both pipelines' local validation and Kaggle results and explain improvement or degradation. |
| Reflection, clarity, and credit | 4 | The report conveys the team's own perspective, lessons and next steps, individual contributions, and credit for outside sources and material AI help. |
| **Total** | **30** |  |