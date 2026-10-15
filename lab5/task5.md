# Lab 5 — Software Life Cycle and Development Methodology

## Project and selected approach

**InPlan** automates individual study planning. Students select courses and a specialization, allocate their credit budget, and track academic progress. Lecturers assign marks, while academic office employees manage model study programmes and generate reports. The project baseline consists of the [requirements questions](../lab2/task2.md), the [functional and non-functional requirements](../lab3/task3.md), and the [use case diagram](../lab4/task4.md).

For InPlan, we propose:

- **Software life cycle model: iterative and incremental development.** Build the system through usable additions and improve existing functionality using feedback.
- **Software development methodology: Agile development organized with Scrum**, supported by code review, automated testing, and continuous integration. Scrum is technically a framework; here it provides the concrete team process requested by the assignment.

The model determines how the product evolves. The methodology determines how the team prioritizes, coordinates, checks, and improves its work. Scrum explicitly supports an iterative and incremental approach, so these choices are compatible. See the [Scrum Guide](https://scrumguides.org/scrum-guide.html#scrum-theory).

## Project characteristics and their implications

The repository describes the intended system, but does not specify actual staffing, team experience, delivery dates, deployment scale, or a technology stack. For this proposal, we assume a university pilot developed by **one student team of approximately 4–6 people**, with basic development skills and mixed experience in testing and deployment. We also assume a fixed course deadline and access to stakeholder feedback or an instructor acting as a stakeholder proxy. These are planning assumptions, not established project facts.

| Aspect | Evidence or assumption for InPlan | Implication for the choice |
| --- | --- | --- |
| **1. Product/project type** | A multi-user academic information system with three user groups. Its central problems are course selection, academic rules, budget calculations, and access to records (FR-01–FR-21; NFR-01–NFR-09). | Demonstrating realistic workflows helps users validate the rules and interface. Short iterations expose misunderstandings before they spread to reporting and progress calculations. |
| **2. Project scale** | Lab 3 lists 28 functional and 20 non-functional requirements, including optional features and exclusions. Lab 4 groups the behaviour into three functional areas. We assume an initial pilot at one university; user counts remain unknown. | A single backlog and integrated product are appropriate for this bounded scope. Incremental delivery makes it manageable without introducing coordination across multiple teams. Requirement counts do not establish workload capacity. |
| **3. Team size** | The assumed team has 4–6 members who collectively cover interface, application logic, storage, and testing. | One Scrum Team can coordinate directly and deliver complete user workflows. Separate analysis, implementation, and testing departments would introduce unnecessary handoffs at this scale. |
| **4. Team competence** | We assume basic programming competence but uneven experience with academic rules, authorization, and reliable data updates. | Small changes, peer review, paired work on unfamiliar areas, and regular retrospectives support learning. A shared completion checklist makes quality expectations explicit instead of relying on individual experience. |
| **5. Business factors and bureaucracy** | The academic office is a stakeholder, while students and lecturers have different needs. Lab 2 asks about eligibility, changes after courses start, and course constraints. Actual approval procedures are unspecified. | A designated Product Owner should resolve competing priorities and obtain academic-office decisions on rules. Regular reviews provide feedback, while documented rule decisions preserve accountability. The assumed course deadline makes scope prioritization essential. |
| **6. Artifacts necessity** | Requirements and a use case diagram already exist. Access restrictions, credit calculations, and specialization checks need verifiable interpretations. | Keep these artifacts current and link backlog items to requirement IDs, acceptance examples, and test evidence. Iterative development should maintain useful documentation as behaviour changes. |
| **7. Technological factors** | Browser access is requested in NFR-15; consistency, persistence, and modifiable academic rules appear in NFR-07–NFR-09 and NFR-17. No framework, database, or external integration is selected. | Integrate interface, logic, and storage early, then rerun checks after each change. Validate uncertain implementation choices through small technical experiments. The proposed process does not depend on an invented stack or integration. |

## 1. Software life cycle model: iterative and incremental

### Why this model fits InPlan

**The requirements provide a direction but still need clarification.** For example, FR-13 requires preventing budget overruns, while Lab 2 asks which restrictions apply to course selection. The team needs agreed examples of valid and invalid plans before implementing those rules. A working planning workflow lets the academic office inspect the consequences of its decisions and correct misunderstandings early.

**The product has natural increments with observable value.** Course browsing can be demonstrated before academic reporting is complete. Plan creation then adds value to the catalogue, and marks later enable meaningful progress tracking. Each increment extends an integrated system; it is not just a separate database or an unfinished interface.

**The same rules affect several features.** Credits influence plan validation and progress; marks feed progress and reports. Short integration cycles reveal inconsistencies while the affected change is still small. NFR-08 makes this especially relevant: correct individual screens are insufficient if their calculations disagree.

**A fixed deadline requires visibility into usable results.** An early integrated version shows what actually works. If progress is slower than expected, the team can defer Should Have and Could Have items before they displace mandatory functionality. Frequent delivery and adaptation also align with the [Agile Manifesto principles](https://agilemanifesto.org/principles.html).

### How the life cycle would work

Start with a short shared understanding of the system boundary, roles, academic terminology, data relationships, and major risks. Then repeat the following cycle for each selected workflow:

1. Clarify its requirements with concrete examples and acceptance criteria.
2. Design the necessary interface, data, and component interactions.
3. Implement and integrate the workflow, including its applicable access and validation rules.
4. Test the new behaviour and rerun checks for previously delivered functionality.
5. Make the usable increment available in a test environment and review it with relevant stakeholders.
6. Update requirements, priorities, and the next iteration using the feedback.

Deployment to real users is a separate release decision based on readiness and the university's constraints. After release, defects and academic-rule changes return to the same backlog. Database changes require migration and recovery checks so that improvements preserve existing study plans and marks.

### Example sequence of product increments

This is a proposed dependency order, not a delivery estimate. An increment below may require several Sprints, each delivering a smaller usable result.

| Increment | Usable outcome and requirement coverage | Feedback or risk addressed |
| --- | --- | --- |
| **1. Secure course discovery** | A student can sign in and inspect available courses and their details (FR-01–FR-02), with the relevant authentication and access protections from NFR-01–NFR-06. Start with agreed test catalogue data. | Students check whether credits, costs, and course information are understandable. The team proves that interface, application logic, and storage work together. |
| **2. Validated individual study planning** | Students select a specialization, add/remove courses, see credit and requirement checks, and allocate their budget (FR-03–FR-13). Include data validation, consistency, and persistence (NFR-07–NFR-09). | The academic office checks missing-course and insufficient-credit cases. Budget boundary checks verify that an over-budget change is rejected without corrupting the saved plan. |
| **3. Academic administration and progress** | Academic office employees create model programmes; authorized lecturers assign marks; students view marks and specialization progress (FR-14–FR-19). Enforce the relevant role and ownership restrictions. | Stakeholders verify programme definitions, grade visibility, and how completed courses contribute to progress. |
| **4. Reporting and release completion** | Academic office employees generate reports by field and specialization (FR-20–FR-21). Verify results against known academic records and complete release-wide acceptance checks. | Confirm that reports and student progress use consistent data. Check the complete mandatory scope before release. |

Agree on the catalogue and specialization rules before implementing dependent planning checks; the later programme-management interface must preserve those definitions. Optional improvements, such as filtering and recommendations (FR-25–FR-26), can follow according to priority and capacity. Mandatory protections apply from the first increment that exposes the relevant data or operation.

All Must Have requirements remain in the intended release scope. Intermediate demonstrations do not justify dropping them. The exclusions concerning unconfirmed automatic enrolment and offline operation (FR-28 and NFR-20) also remain unchanged.

### Comparison with other life cycle models

| Alternative | Why it is less suitable for this project |
| --- | --- |
| **Sequential Waterfall** | A largely fixed requirements baseline would be difficult to justify while academic rules and user workflows still need clarification. Discovering a misunderstanding after implementing dependent features would cause broader rework. It would be more attractive if requirements and acceptance procedures were stable and contractually fixed. |
| **V-model** | Its emphasis on matching requirements to verification is useful, and we adopt that traceability. However, a predominantly sequential application would offer less flexibility for the feedback expected here. No formal certification requirement is stated that would justify choosing it as the overall model. |
| **Spiral** | Risk-driven cycles could help if InPlan involved major technical uncertainty or high-risk integrations. Neither is established in the repository. For the assumed small pilot, targeted experiments and a risk list are more proportionate than a formal risk-analysis cycle for every expansion. |
| **Prototyping alone** | Interface prototypes can clarify course selection, but cannot establish reliable persistence, authorization, and consistent calculations. Use prototypes within iterations, then implement and verify production-quality functionality. |

## 2. Development methodology: Agile with Scrum

### Why Scrum fits InPlan

InPlan needs a shared priority order across three stakeholder groups. Otherwise, developers could independently finish catalogue screens, lecturer tools, and reports without producing a complete student workflow. A common Product Goal and a focused Sprint Goal help the team deliver something that can be inspected together.

We propose **two-week Sprints** as an initial cadence: long enough to integrate and verify a small workflow, but short enough to receive feedback during the assumed course project. The team should select scope using its actual availability and observed progress; the duration does not imply that every increment in the table takes two weeks.

The following is a proposed InPlan working arrangement, using the accountabilities and events defined in the [Scrum Guide](https://scrumguides.org/scrum-guide.html).

- **Product Owner:** designate one person to order the backlog, maintain the release scope, and clarify rules with academic office representatives while considering students and lecturers. In the course setting, a team member can act as a proxy, recording which decisions still need validation.
- **Scrum Master:** designate a team member to help the group use Scrum, resolve coordination problems, and follow through on process improvements. This need not be a separate full-time position.
- **Developers:** the team jointly owns implementation, testing, integration, and documentation. Work allocation follows the Sprint Goal rather than permanent component silos.

### Working rhythm

At **Sprint Planning**, choose one demonstrable goal, such as allowing a student to edit a budget-valid study plan. Select related backlog items and agree on examples of acceptable behaviour. Hold a **15-minute Daily Scrum** on each working day to coordinate progress and blockers. Continue refining upcoming work as questions are answered.

At the **Sprint Review**, inspect the working result with the relevant users or stakeholder proxy and revise priorities. At the **Sprint Retrospective**, select a concrete improvement, such as adding authorization checks earlier after an access-control defect. The review provides feedback; it does not replace testing or act as a mandatory release gate.

For the assumed small team and two-week cadence, start with about one hour of planning, 45 minutes of review, and 30 minutes of retrospective, adjusting within Scrum's event limits when necessary. These are proposed meeting lengths, not measured team practice.

### Artifacts and engineering discipline

Maintain a Product Backlog with a Product Goal, a Sprint Backlog with a Sprint Goal, and a usable Increment satisfying a shared Definition of Done. For InPlan, the proposed Product Goal is to let students manage valid individual plans while authorized staff maintain academic records and obtain consistent reports.

Each backlog item should link to the relevant FR/NFR IDs and include acceptance examples. Preserve the requirements, use case diagram, important academic-rule decisions, test results, and release instructions in version control. GitHub issues or a simple board can track work; a separate management platform is unnecessary for the assumed team.

An item is **Done** when:

1. Its agreed behaviour and relevant requirements are implemented and verified.
2. Another team member has reviewed the change, and automated checks pass.
3. Applicable access, validation, and persistence checks pass, including failure cases.
4. It integrates with earlier functionality without known blocking regressions.
5. Affected documentation and test-environment deployment instructions are current.

For example, a budget item needs checks at and above the available limit; a marks item needs checks that unauthorized lecturers cannot modify a mark. Continuous integration should run these checks after changes. Peer review and paired work on difficult rules complement Scrum, which does not prescribe the implementation techniques.

For performance requirements NFR-11–NFR-13, first agree on representative data volume and concurrent-user workload. Then measure the stated two-second operation and ten-second report targets under that workload. Without it, the team cannot claim those targets are verified. Retain the priorities recorded in Lab 3 when planning these checks.

### Comparison with other development approaches

| Alternative | Assessment for InPlan |
| --- | --- |
| **Kanban** | A credible option, especially for later maintenance with unpredictable incoming requests. For the assumed initial course project, Scrum's explicit goals and scheduled reviews provide useful coordination and feedback. Kanban could also provide a review cadence, but the team would need to define that arrangement itself. |
| **Extreme Programming (XP)** | Its testing, integration, and collaboration practices are useful for reliable academic calculations. Scrum provides our primary structure for stakeholder priorities and delivery; selected XP practices strengthen implementation. The repository does not establish that the team can sustain all XP practices, such as an on-site customer. |
| **Rational Unified Process (RUP)** | Its iterative, architecture-focused approach and requirements traceability are useful for InPlan's connected academic rules. RUP can be tailored to a small team, but selecting and maintaining the necessary roles and artifacts adds process setup. Our proposed Scrum arrangement retains explicit requirements and design decisions with fewer prescribed responsibilities. |
| **Microsoft's Synch-and-Stabilize process (MSS)** | MSS combines planning, development, and stabilization with frequent synchronization and milestone releases. Its program manager, developer, and tester roles coordinate interdependent features; developer–tester pairs provide independent checks. This is useful for keeping plans, credits, marks, and reports consistent. However, the staffing and milestone structure described by Rockwood would need adaptation for our assumed 4–6-person team. We adopt continuous integration and stabilization checks without adopting the full MSS organization. |
| **Team Software Process (TSP)** | TSP builds on the Personal Software Process (PSP), using iterative cycles, explicit roles, process scripts, plans, reviews, and measurement. Rockwood describes its academic variant, TSPi, where members combine development with team leadership, development, planning, quality/process, and support responsibilities. It is a credible fit for a small novice team and could improve defect prevention and estimation. For InPlan, adopting its detailed scripts, records, and process training would require capacity beyond our proposed Scrum routine. Prefer TSP if learning a disciplined engineering process or collecting reliable process measurements becomes a primary project objective. |

The MSS and TSP descriptions follow Justin Rockwood's *Choose Your Weapon Wisely*, Sections 2.3–2.4, printed pp. 7–15 (PDF pages 15–23 in the supplied document). MSS here means **Microsoft's Synch-and-Stabilize**, which the paper distinguishes from Microsoft Solutions Framework (MSF).

### Conditions and limitations

The recommendation depends on regular feedback, a manageable team size, and authority to adjust backlog priorities. If academic staff are unavailable, record unresolved rules and seek proxy feedback without presenting it as university approval. If the team cannot maintain the core Scrum events and accountabilities, a simpler Kanban process would be a more honest and practical choice. If deployment introduces strict approval gates or major integration risks, add the necessary release controls and reassess the life cycle assumptions.

With the stated assumptions, iterative and incremental development addresses InPlan's evolving academic rules and connected workflows, while Scrum gives the team a concrete way to prioritize and inspect progress. Testing, traceable decisions, and incremental integration make the approach suitable for a system where incorrect plans, budgets, or marks would directly affect users.

## 3. Completed Rockwood process selection table

This completes the **Appendix A — Question Tally Sheet** from Justin Rockwood's *Choose Your Weapon Wisely*, Carnegie Mellon University, using the supplied PDF. The blank table is on printed p. 35 (PDF page 43); its scoring matrices are in Sections 3.1–3.4, printed pp. 23–33. The columns compare RUP, MSS, TSP, XP, and Scrum. Kanban is discussed above but is not part of this questionnaire.

Rockwood assigns **1 for a relative weakness, 2 for a neutral fit, and 3 for a relative strength** under the selected answer. Each table row below uses the corresponding matrix unchanged. Totals are simple column sums over all 11 questions, with a maximum of 33; we introduce no additional criterion weights.

The answers describe a **provisional InPlan pilot scenario**, not a survey of the actual team. Staffing, code size, experience percentages, and organizational preferences are not recorded in the repository. In particular, basic programming skills do not establish the paper's definition of experience: prior work in the technology domain, similar systems, and communication skills. We conservatively use the novice category until that experience is confirmed.

| Question | Selected answer and InPlan rationale | RUP | MSS | TSP | XP | Scrum | Matrix page |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Team Size | **a — Fewer than 10.** The assumed single team has 4–6 members, including development and testing responsibilities. | 1 | 1 | 3 | 3 | 3 | 23 |
| Total Developers | **a — Fewer than 40.** The same small team develops the whole pilot; no additional teams are assumed. | 2 | 2 | 2 | 2 | 2 | 24 |
| Product Size and Complexity | **a — Small product, hundreds to a few thousand lines.** Assume a limited pilot implementation for this scoring scenario. This is not a code-size estimate derived from the requirement count. | 1 | 1 | 1 | 3 | 3 | 25 |
| Competent and Experienced Developers | **a — Below 10%.** Conservatively assume no confirmed member meets all three experience conditions in Rockwood's question. The actual percentage needs verification. | 1 | 1 | 3 | 1 | 1 | 26 |
| Level of Hacker Sentiment | **b — Plan enough before coding.** Clarify roles, data relationships, and critical academic rules, then learn from working increments instead of exhaustively designing every detail first. | 2 | 2 | 1 | 2 | 2 | 27 |
| Management Style | **a — Macro-management.** Assume the team chooses implementation details within agreed goals and constraints, without a manager prescribing each development step. | 2 | 3 | 1 | 3 | 3 | 28 |
| Organization-Wide Processes | **b — Somewhat important.** Assume the team needs continuity and documented decisions, but no organization-wide process standardization programme. | 2 | 2 | 2 | 2 | 2 | 29 |
| New Process Adoption | **b — A reasonably mature process is sufficient.** The pilot has no stated requirement for adoption evidence across many market segments. | 2 | 2 | 2 | 2 | 2 | 30 |
| Type of Product | **d — Neither life- nor mission-critical application.** Score the proposed educational pilot, not an established university production system on which operations already depend. Academic-data correctness still matters. | 2 | 2 | 2 | 2 | 2 | 31 |
| Requirements Stability | **a — Emergent/changing.** For the pilot, assume stakeholder feedback can materially revise the unanswered academic rules and workflows identified in Lab 2. The repository does not establish an actual change rate. | 2 | 2 | 2 | 3 | 3 | 32 |
| Requirements Traceability | **b — Somewhat important.** FR/NFR identifiers must connect promised behaviour to implementation and acceptance evidence; no formal certification requirement is stated. | 2 | 2 | 2 | 1 | 1 | 33 |
| **Totals** | **Unweighted sum of the 11 matrix rows** | **19** | **20** | **21** | **24** | **24** | — |

Page numbers in the final column are the document's printed page numbers; add 8 to obtain the PDF viewer page. For traceability, the answer letters follow the matrix on p. 33: the explanatory bullets beneath it are mislabelled c/d/e rather than a/b/c.

### Interpretation for InPlan

**XP and Scrum tie at 24**, followed by TSP at 21, MSS at 20, and RUP at 19. The table supports considering both agile approaches; it does not establish Scrum as a unique numerical winner. We retain Scrum for organizing stakeholder priorities and integrated delivery, complemented by XP practices for testing, integration, and shared code ownership. This is a project-specific choice between the tied candidates.

The weak scores for Scrum and XP on **experience** and **traceability** identify work the team must address. Guided reviews and paired work on unfamiliar areas can support less experienced members, while links between requirements, backlog items, changes, and acceptance checks preserve traceability. These practices do not change the paper's scores or prove that the team already has the necessary experience. TSP remains a serious alternative because its explicit guidance directly addresses novice-team needs.

The ranking is sensitive to assumptions. If product size instead falls into **category b** and management needs **category b** structure, replacing just those two rows gives **RUP 21, MSS 21, TSP 23, XP 22, and Scrum 22**. TSP then leads. Actual scope and the team's ability to self-manage should therefore be checked before treating the provisional recommendation as a firm decision.

Finally, this is the paper's historical scoring model, not a current benchmark or a probability of project success. We preserve it for the assignment without adopting its historical statements about process maturity, scaling limits, or Scrum artifacts as present-day rules. The proposed Scrum operation in Section 2 follows the linked Scrum Guide; the completed questionnaire provides additional evidence and exposes assumptions rather than replacing project judgment.
